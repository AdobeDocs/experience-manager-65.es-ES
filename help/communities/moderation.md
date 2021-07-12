---
title: Consola de moderación
seo-title: Consola de moderación
description: Cómo acceder a la consola Moderación
seo-description: Cómo acceder a la consola Moderación
uuid: d3b8a160-85b2-43f4-9891-5fafa8c48c5f
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 404582ab-bb4c-4775-9ae3-17356d376dca
docset: aem65
role: Admin
exl-id: 829da16a-4083-43c1-857d-f2666b363bfc
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '2110'
ht-degree: 4%

---

# Consola de moderación {#moderation-console}

En AEM Communities, la [moderación masiva del contenido de la comunidad](/help/communities/moderate-ugc.md) es posible tanto desde los entornos de autor como de publicación por parte de los administradores y los moderadores de la comunidad (miembros de la comunidad de confianza asignados como moderadores).

Los administradores y moderadores de la comunidad también pueden realizar [moderación en contexto](/help/communities/in-context.md) en el entorno de publicación.

Una función de todos los [sitios de la comunidad](/help/communities/sites-console.md) es un elemento de menú `Administration` disponible para los usuarios que inician sesión con privilegios administrativos. El enlace `Administration` proporciona acceso a la consola Moderación .

Desde la consola Moderación , los administradores y los moderadores de la comunidad tendrán acceso a todo el contenido generado por el usuario (UGC) para el que tengan permiso de moderación. Si se permite moderar varios sitios, es posible ver los anuncios de todos los sitios o filtrarlos según los sitios de comunidades seleccionadas.

Para obtener información más detallada, visite [Administración de usuarios y grupos de usuarios](/help/communities/users.md).

La consola Moderación admite:

* Realización de tareas de moderación de forma masiva.
* Buscando UGC.
* Visualización de detalles de UGC.
* Visualización de los detalles del autor de UGC.

Solo se pueden realizar tareas de moderación cuando se inicia sesión como administrador o como miembro con ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`.

## Acceso al entorno de publicación {#publish-environment-access}

El acceso a la consola Moderación desde un sitio de comunidad publicado se realiza mediante un vínculo de Administración que aparece cuando un moderador de la comunidad ha iniciado sesión.

![publishweretail](assets/publishweretail.png)

Al seleccionar el vínculo Administración , aparece la consola Moderación :

![moderación-consola-publicar](assets/moderation-console-publish.png)

## Acceso al entorno de creación {#author-environment-access}

En el entorno de creación, para llegar a la consola Moderación

* En la navegación global, seleccione **[!UICONTROL Communities]** > **[!UICONTROL Moderación]**.

Solo se pueden realizar tareas de moderación cuando se inicia sesión como administrador o como miembro con [permisos de moderador](/help/communities/in-context.md#identifyingtrustedmembers). El único contenido de la comunidad que se muestra es el que el miembro que ha iniciado sesión puede moderar.

>[!NOTE]
>
>UGC del entorno de publicación solo será visible para el autor si el SRP elegido implementa un almacén común. Por ejemplo, de forma predeterminada, el almacenamiento es JSRP, que no es un almacén común para la creación y publicación. Consulte [Almacenamiento de contenido de la comunidad](/help/communities/working-with-srp.md).

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## Interfaz de usuario de la consola de moderación {#moderation-console-ui}

Dejando a un lado el carril de navegación izquierdo (que aparece en el autor, pero no en la publicación), la interfaz de usuario de moderación tiene las siguientes áreas principales:

* **[Barra de navegación superior](#top-navigation-bar)**
* **[Barra de herramientas](#toolbar)**
* **[Área de contenido](#content-area)**

### Barra de navegación superior {#top-navigation-bar}

La barra de navegación superior es constante para todas las consolas. Para obtener más información, consulte [Gestión básica](/help/sites-authoring/basic-handling.md).

### Barra de herramientas {#toolbar}

La barra de herramientas, situada debajo de la barra de navegación superior, proporciona el siguiente interruptor de alternancia en el lado izquierdo:

* [El ](/help/communities/moderation.md#filterrail)
carril de filtro abre un carril que permite elegir las propiedades en las que filtrar el contenido.

La barra de herramientas, situada debajo de la barra de navegación superior, proporciona el siguiente interruptor de alternancia en el lado izquierdo:

![alterneswitch](assets/toggleswitch.png)

[El ](/help/communities/moderation.md#filterrail)
carril Filtro abre un carril, al seleccionar Buscar, que permite elegir las propiedades en las que filtrar el contenido.

![filtro](assets/filterrail.png)

### Área de contenido {#content-area}

El área de contenido contiene información para el UGC publicado:

* UGC publicado
* Nombre del miembro
* avatar de miembro
* Ubicación del anuncio.
* Cuando se publicó.
* Número de respuestas a la publicación.
* [](/help/communities/moderate-ugc.md#sentiment) Opinión asociada a la publicación
* Si se aprueba, se muestra una marca de verificación.
* Si hay un accesorio, se muestra un clip.

>[!NOTE]
> 
>El área de contenido incluye un *desplazamiento infinito*, lo que significa que le permitirá continuar desplazándose hasta que haya llegado al final del contenido. La barra de herramientas permanece en una posición fija y visible sobre el área de contenido aunque se desplace.

### Carril de filtro {#ootbfilters}

![carril de filtro abierto](assets/open-filterrail.png)

El icono del panel lateral abre el carril de filtro. El carril de filtro, que aparece a la izquierda del área de contenido, proporciona diferentes filtros, cada uno de los cuales tiene un efecto inmediato en el UGC al que se hace referencia y que aparece en el área de contenido.

Los filtros dentro de cada categoría son **OR**&#39;d juntos, y los filtros en diferentes categorías son **AND**&#39;d juntos.

Por ejemplo, si marca **Pregunta** y **Respuesta**, verá contenido que puede ser una **Pregunta** *o* y una **Respuesta**.

Sin embargo, si marca **Pregunta** y **Pendiente**, solo verá contenido que sea una **Pregunta** y esté **Pendiente**.

>[!NOTE]
>
>Los moderadores de la comunidad pueden marcar los filtros predefinidos en la interfaz de usuario de la consola de moderación. Como estos filtros se anexan hacia el final de la dirección URL (como parámetros de cadena de consulta), los moderadores pueden volver a los filtros marcados más adelante y también compartir estos vínculos.

![searchicon](assets/searchicon.png)

Cuando el carril del filtro está abierto, el icono Buscar alterna el panel lateral cerrado. Sin embargo, para cerrar el carril del filtro y ver únicamente el contenido generado por el usuario, haga clic en el icono Buscar y seleccione la opción Solo contenido .

#### Ruta de contenido {#content-path}

La ruta de contenido limita la referencia UGC mostrada a los anuncios colocados en el repositorio de contenido especificado.

![content-path](assets/content-path.png)

#### Búsqueda de texto {#text-search}

La búsqueda de texto limita el UGC referenciado mostrado a las publicaciones en las que contiene el texto introducido.

![text-search](assets/text-search.png)

#### Sitio {#site}

El sitio limita el UGC referenciado mostrado a los anuncios de los sitios de la comunidad seleccionados. Si no hay sitios marcados, entonces se muestran todas las referencias a UGC.

![panel del sitio](assets/site-panel.png)

>[!NOTE]
>
>Cuando un administrador accede a la consola de moderación masiva, se muestran todas las referencias a UGC, incluidos los sitios no creados con el [asistente de creación de sitios](/help/communities/sites-console.md), como los ejemplos de Geometrixx.
>
>Cuando un miembro de la comunidad de confianza accede a la consola de moderación masiva en la publicación, solo se muestran las referencias a UGC creadas para sitios de la comunidad que el miembro está autorizado a moderar y pueden filtrarse con el filtro Sitio .

#### Tipo de contenido {#content-type}

El tipo de contenido limita el UGC referenciado mostrado a los anuncios del tipo de recurso seleccionado. Se pueden seleccionar uno o más de los siguientes tipos. Todos los tipos se muestran si no se selecciona ninguno.

* **Comentario**
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

![tipos de contenido](assets/content-types.png)

#### Tipos de contenido adicionales {#additional-content-types}

Para añadir recursos adicionales a los que filtrar:

* Inicie sesión en la instancia de autor como administrador.
* Abra [Consola Web](https://localhost:4502/system/console/configMgr).
* Busque `AEM Communities Moderation Dashboard Filters`.
* Seleccione la configuración que desea abrir en el modo de edición.
* Introduzca el ResourceType de un componente en el que filtrar:

   * Por ejemplo, para filtrar los componentes Votación incluidos, introduzca:

      `Voting=social/tally/components/hbs/voting`
   ![additional-contenttype](assets/additional-contenttype.png)

* Seleccione Guardar.
* Actualice la consola Comunidades - Moderación .

El resultado es un nuevo filtro seleccionable para `Voting` en el grupo de filtros `Content Type`.

Cuando se selecciona ese filtro, el contenido del tablero mostrará UGC que coincida con cualquiera de los Tipos de recursos introducidos.

#### Estado {#status}

El estado limita el UGC referenciado mostrado a las publicaciones del estado seleccionado, que pueden ser una o más de Pendiente, Aprobado, Denegado o Cerrado, así como Borrador o Programado para Artículos de Blog y Contestado o No Respondido para Preguntas de Control de Calidad. Si no se selecciona ninguno, se muestran todos.

>[!NOTE]
>
>Si solo se selecciona el estado No respondido , el moderador verá todo el contenido (para todos los tipos de contenido) excepto las preguntas respondidas. Esto se debe a que la propiedad responsable de la pregunta contestada no existe en el caso de preguntas no respondidas y otro contenido como tema del foro, artículo del blog o comentarios.

![estados](assets/statuses.png)

#### Indicación {#flagging}

El marcado limita el UGC al que se hace referencia mostrado a las publicaciones que están marcadas u ocultas.

Una vez marcado un fragmento de contenido, permanece marcado hasta que se desmarca ese fragmento de contenido seleccionando de nuevo el botón **Flag**. Tenga en cuenta que no hay niveles de indicador, como importante o de seguimiento.

![marcar](assets/flagging.png)

#### Miembros {#members}

Los miembros limitan el UGC referenciado que se muestra en UGC publicado por el nombre de miembro introducido.

![miembros](assets/members.png)

#### Enviado en el último {#posted-in-the-last}

Publicado en Último limita el UGC referenciado mostrado a los anuncios realizados en la última hora, día, semana, mes o año.

![post-last](assets/posted-last.png)

#### Opinión {#sentiment}

[](/help/communities/moderate-ugc.md#sentiment) La opinión limita el UGC referenciado mostrado a las publicaciones con un valor de opinión positivo, negativo o neutro.

![opinión](assets/sentiment.png)

## Filtros personalizados {#custom-filters}

Aparte de los filtros predeterminados en [Carril de filtro](/help/communities/moderation.md#ootbfilters), se pueden agregar filtros personalizados adicionales sobre metadatos a la interfaz de usuario de moderación. Los desarrolladores pueden utilizar el código de muestra de Github para ampliar los filtros de interfaz de usuario de moderación existentes.

![custom-tag-filter](assets/custom-tag-filter.png)

El [proyecto de muestra](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/main/aem-communities-moderation-filter) en Github implementa el filtro Etiqueta para filtrar la lista UGC en función de si las etiquetas específicas se aplican al contenido generado por el usuario. Puede seguir el código de muestra y crear filtros análogos para otros campos de metadatos UGC similares.

Para instalar el ejemplo para el filtro Etiquetas :

1. Abra el administrador de paquetes en la instancia de AEM Author ([https://[aem-author]:4502/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp)) y AEM Publish ([https://[aem-publish]:4503/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp)).
1. Cree el paquete `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` desde el código de Github, e instale y habilite lo mismo.
1. Abra la consola de paquetes en la instancia de AEM Author ( `https://[aem-author]:4502/system/console/bundles`) y en la instancia de AEM Publish ( `https://[aem-publish]:4503/system/console/bundles`).
1. Cree el paquete ` [com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar` desde Github, e instale y habilite lo mismo.
1. Vaya al nodo **/apps/social/moderation/facets** en AEM Author ([https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets)) y AEM Publish ([https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets)).
1. Agregue un usuario técnico **communities-Utility-reader** con permisos `jcr:read`.

Para exponer los filtros personalizados en sitios de la comunidad existentes:

1. Editar `Clientlibs` de la página de moderación existente `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * Añadir nueva categoría `cq.social.hbs.moderation.v2.`

1. Ir a `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * Establecer en nuevo componente `sling:resourceType = social/moderation/v2/filters.`

1. Ir a `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * Configure el nuevo componente `sling:resourceType = social/moderation/v2/modcontainer`.

## Acciones de moderación {#moderation-actions}

[Las ](/help/communities/moderate-ugc.md#moderation-actions) acciones de moderación se pueden realizar en una o más selecciones realizadas en el área de contenido o al ver los detalles del contenido.

Para moderar las publicaciones de forma masiva, en el área de contenido, haga clic en el icono Seleccionar (![selector](assets/selecticon.png)) de una publicación, que aparece al pasar el ratón (escritorio) por encima o presionando y sosteniendo un dedo en la publicación (móvil). Al hacerlo, entrará al modo de selección múltiple y ahora puede seleccionar las publicaciones siguientes que se van a moderar por lotes simplemente haciendo clic en ellas. Utilice los botones mostrados en la barra de herramientas para realizar acciones de moderación en los anuncios seleccionados. Todas las acciones solicitarán confirmación.

Para moderar una sola publicación en el área de contenido, pase el ratón sobre ella (escritorio) o presione y mantenga presionado un dedo sobre la publicación (móvil) para que aparezcan botones en la publicación. Cuando se trabaja con un solo detalle de contenido, solo una acción de eliminación solicitará confirmación.

### Moderación de varias publicaciones {#moderating-multiple-posts}

Especifique el modo de selección masiva haciendo clic en el icono `Select` de una publicación:

![icono de selección](assets/select-icon.png)

Para salir del modo de selección masiva, seleccione el icono Cancelar (x) en la barra de herramientas:

Las acciones de moderación que se pueden realizar en varias publicaciones son:

* Denegar
* Eliminar
* Cierre o vuelva a abrir las publicaciones

Los iconos que permiten estas acciones solo aparecen en la barra de herramientas cuando se seleccionan varios anuncios.

![bulkmoder](assets/bulkmoderate.png)

### Moderación de una sola publicación {#moderating-a-single-post}

En el modo de selección única, es posible:

* Para ver los detalles del usuario, seleccione su nombre.
* Para ver la publicación en contexto, seleccione el vínculo a la publicación.
* [respuesta](#reply)
* [Permitir](#allow)
* [Denegar](#deny)
* [Eliminar](#delete)
* [Cerrar](#close)
* Ver [Historial de moderación](#moderation-history)
* [Ver detalles](#viewdetails)

Presente en la vista de tarjeta sobre los iconos de acción de moderación es el texto de la publicación y debajo hay datos que indican:

* En caso afirmativo, precedido del número de respuestas.
* Si se ha marcado.
* Si se ha aprobado.
* Cuando se publicó el UGC.

![singleselectmode](assets/singleselectmode.png)

#### respuesta {#reply}

![respuesta](assets/reply.png)

Al trabajar con un solo anuncio, aparecerá un icono Responder si el tipo UGC admite respuestas y está configurado para permitir respuestas.

#### Permitir {#allow}

![permitir](assets/allow.png)

Cuando se trabaja con un solo anuncio, el icono Permitir aparecerá cuando el anuncio se haya marcado o rechazado. Si se marca, al seleccionar Permitir se borrarán todos los indicadores.

#### Denegar {#deny}

![denegar](assets/deny.png)

La acción de moderación **Denegar** solo está disponible para contenido moderado y no aparece en contenido no moderado excepto en modo de selección múltiple.

El contenido que no está moderado siempre se aprueba.

El contenido moderado inicialmente entra en un estado Pendiente y más tarde se puede modificar para ser aprobado o rechazado.

El contenido que deja el estado pendiente nunca puede volver a un estado pendiente. El contenido marcado como aprobado o rechazado se puede cambiar a un estado diferente en cualquier momento.

#### Eliminar {#delete}

![delete](assets/delete.png)

En el modo de selección única o masiva, puede seleccionar elementos y eliminarlos. La acción de eliminar genera un cuadro de diálogo de confirmación. Una vez eliminados, esos elementos desaparecen inmediatamente del área de contenido. **Una vez eliminado UGC, se elimina permanentemente del repositorio y no se puede recuperar** más adelante.

#### Cerrar {#close}

![cerrar](assets/close.png)

Al trabajar con un solo anuncio, aparecerá un icono Cerrar si el tipo UGC admite la capacidad de evitar más anuncios para ese recurso.

#### Historial de moderación {#moderation-history}

![moderación](assets/moderation.png)

Al trabajar con una sola publicación, aparecerá un icono Historial de moderación al pasar el ratón por encima. Al seleccionar el icono, se mostrará un panel que contiene un historial de acciones realizadas con respecto al anuncio UGC.

Para volver a la visualización del área de contenido de varios anuncios UGC, seleccione la X en la esquina superior derecha del panel de detalles de la vista.

Por ejemplo:

![moderación-historial](assets/moderation-history.png)

#### Ver detalles {#view-detail}

![ver](assets/view.png)

Al trabajar con una sola publicación, se pueden ver más detalles abriendo el UGC en modo de detalle.

Para ello, pase el ratón sobre la publicación para mostrar el icono `View Detail` y selecciónelo para mostrar un panel que contenga más detalles de la publicación.

Para volver a la visualización del área de contenido de varios anuncios UGC, seleccione la X en la esquina superior derecha del panel de detalles de la vista.

Por ejemplo:

![view1](assets/view1.png)
