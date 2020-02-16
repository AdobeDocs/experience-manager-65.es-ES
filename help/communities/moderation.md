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
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65

---


# Consola de moderación{#moderation-console}

En las comunidades AEM, los administradores y los moderadores de la comunidad (miembros de la comunidad de confianza asignados como moderadores) pueden [moderar de forma masiva el contenido](/help/communities/moderate-ugc.md) de la comunidad desde los entornos de creación y publicación.

Los administradores y los moderadores de la comunidad también pueden realizar una moderación [en contexto](/help/communities/in-context.md) en el entorno de publicación.

Una característica de todos los sitios [de](/help/communities/sites-console.md) comunidad es un elemento de `Administration`menú disponible para los usuarios que inician sesión con privilegios administrativos. El `Administration`vínculo proporciona acceso a la consola Moderación.

Desde la consola Moderación, los administradores y los moderadores de la comunidad tendrán acceso a todo el contenido generado por el usuario (UGC) para el que tengan permiso de moderación. Si se permite moderar varios sitios, es posible ver anuncios en todos los sitios o filtrar por sitios de comunidades seleccionados.

Para obtener información más detallada, visite [Administración de usuarios y grupos](/help/communities/users.md)de usuarios.

La consola Moderación admite:

* realizar tareas de moderación de forma masiva
* buscar UGC
* visualización de detalles de UGC
* visualización de los detalles del autor de UGC

Sólo cuando se inicia sesión como administrador o como miembro con ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`, se pueden realizar tareas de moderación.

## Acceso al entorno de publicación {#publish-environment-access}

El acceso a la consola Moderación desde un sitio de comunidad publicado se realiza a través de un vínculo Administración que aparece cuando un moderador de la comunidad ha iniciado sesión.

![publishweretail](assets/publishweretail.png)

Al seleccionar el vínculo Administración, aparece la consola Moderación:

![moderationconsole-publish](assets/moderationconsole-publish.png)

## Acceso al entorno de creación {#author-environment-access}

En el entorno de creación, para acceder a la consola Moderación

* desde la navegación global: **Navegación, Comunidades, Moderación**

Sólo cuando se inicia sesión como administrador o como miembro con ` [moderator permissions](/help/communities/in-context.md#identifyingtrustedmembers)`, se pueden realizar tareas de moderación. El único contenido de la comunidad que se muestra es aquél que el miembro que ha iniciado sesión puede moderar.

>[!NOTE]
>
>UGC del entorno de publicación solo estará visible para el autor si el SRP elegido implementa un almacén común. Por ejemplo, de forma predeterminada, el almacenamiento es JSRP, que no es un almacén común para la creación y publicación. Consulte Almacenamiento [de contenido de la comunidad](/help/communities/working-with-srp.md).

![moderationconsoleauthor](assets/moderationconsoleauthor.png)

## IU de la consola de moderación {#moderation-console-ui}

Dejando de lado el carril de navegación izquierdo (que aparece en el autor, pero no en la publicación), la interfaz de usuario de moderación tiene las siguientes áreas principales:

* **[barra de navegación superior](#top-navigation-bar)**
* **[toolbar](#toolbar)**
* **[área de contenido](#content-area)**

### Top Navigation Bar {#top-navigation-bar}

La barra de navegación superior es constante para todas las consolas. Para obtener más información, consulte Gestión [básica](/help/sites-authoring/basic-handling.md).

### Barra de herramientas {#toolbar}

La barra de herramientas, situada debajo de la barra de navegación superior, proporciona el siguiente conmutador en el lado izquierdo:

* [El carril](/help/communities/moderation.md#filterrail)de filtro abre un carril que permite elegir las propiedades en las que se debe filtrar el contenido.

La barra de herramientas, situada debajo de la barra de navegación superior, proporciona el siguiente conmutador en el lado izquierdo:

![togleswitch](assets/toggleswitch.png)

[El carril](/help/communities/moderation.md#filterrail)de filtro abre un carril, al seleccionar Buscar, que permite elegir las propiedades en las que se debe filtrar el contenido.

![filterrail](assets/filterrail.png)

### Área de contenido {#content-area}

El área de contenido contiene información para UGC publicado:

* UGC publicó
* nombre del miembro
* avatar miembro
* ubicación del anuncio
* cuando se publicó
* número de respuestas al anuncio
* [opinión](/help/communities/moderate-ugc.md#sentiment) asociada a la publicación
* si se aprueba, se muestra una marca de verificación
* si hay un adjunto, se muestra un clip

>[!NOTE]
>
>El área de contenido presenta un desplazamiento ** infinito, lo que significa que le permitirá continuar desplazándose hasta que llegue al final del contenido. La barra de herramientas permanece en una posición fija y visible sobre el área de contenido, incluso mientras se desplaza.

### Carril de filtro {#ootbfilters}

![chlimage_1-212](assets/chlimage_1-212.png)

El icono del panel lateral abre el carril del filtro. El carril del filtro, que aparece a la izquierda del área de contenido, proporciona diferentes filtros, cada uno de los cuales tiene un efecto inmediato en el UGC referenciado que aparece en el área de contenido.

Los filtros dentro de cada categoría están **** Oed juntos, y los filtros en diferentes categorías están **** Yed juntos.

Por ejemplo, si comprueba tanto **Pregunta** como **Respuesta**, verá contenido que es un **Pregunta ***o* una **Respuesta**.

Sin embargo, si marca **Pregunta** y **Pendiente**, solo verá contenido que sea **Pregunta **y que esté **Pendiente**.

>[!NOTE]
>
>Los moderadores de la comunidad pueden marcar los filtros predefinidos en la interfaz de usuario de la consola de moderación. A medida que estos filtros se anexan hacia el final de la dirección URL (como parámetros de cadena de consulta), los moderadores pueden volver más tarde a los filtros marcados y también compartir estos vínculos.

![searchicon](assets/searchicon.png)

Cuando el carril del filtro está abierto, el icono de búsqueda activa el panel lateral cerrado. Sin embargo, para cerrar el carril del filtro y ver únicamente el contenido generado por el usuario, haga clic en el icono Buscar y seleccione la opción Solo contenido.

#### Ruta de contenido {#content-path}

Ruta del contenido limita la UGC de referencia mostrada a los anuncios colocados en el repositorio de contenido especificado.

![content-path](assets/content-path.png)

#### Búsqueda de texto {#text-search}

La búsqueda de texto limita la UGC referenciada mostrada a las publicaciones en las que se incluye el texto introducido.

![chlimage_1-213](assets/chlimage_1-213.png)

#### Sitio {#site}

El sitio limita el UGC referenciado mostrado a los anuncios en los sitios de comunidad seleccionados. Si no hay sitios marcados, se muestran todas las referencias a UGC.

![chlimage_1-214](assets/chlimage_1-214.png)

>[!NOTE]
>
>Cuando un administrador accede a la consola de moderación masiva, se muestran todas las referencias a UGC, incluidos los sitios no creados con el asistente [de creación de](/help/communities/sites-console.md)sitios, como los ejemplos de Geometrixx.
>
>Cuando un miembro de la comunidad de confianza accede a la consola de moderación masiva al publicar, solo se muestran las referencias a UGC creadas para los sitios de la comunidad que el miembro está autorizado a moderar y se pueden filtrar con el filtro del sitio.

#### Tipo de contenido {#content-type}

El tipo de contenido limita el UGC referenciado mostrado a los anuncios del tipo de recurso seleccionado. Se puede seleccionar uno o más de los siguientes tipos. Todos los tipos se muestran si no se selecciona ninguno.

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

Para agregar recursos adicionales en los que filtrar:

* en una instancia de autor
* iniciar sesión como administrador
* abrir consola [web](https://localhost:4502/system/console/configMgr)
* localizar `AEM Communities Moderation Dashboard Filters`
* seleccione la configuración que desea abrir en el modo de edición
* introduzca el ResourceType de un componente en el que filtrar

   * por ejemplo, para filtrar los componentes de voto incluidos, introduzca:
      `Voting=social/tally/components/hbs/voting`

![chlimage_1-215](assets/chlimage_1-215.png)

* seleccionar Guardar
* actualizar la consola Comunidades - Moderación

El resultado es un nuevo filtro seleccionable `Voting`en el grupo de `Content Type` filtros.

Cuando se selecciona ese filtro, el contenido del tablero mostrará UGC que coincida con cualquiera de los ResourceTypes especificados.

#### Estado {#status}

El estado limita el UGC referenciado mostrado a las publicaciones del estado seleccionado, que pueden ser una o más de Pendiente, Aprobado, Denegado o Cerrado, así como Borrador o Programado para Artículos de Blog y Respondido o No Respondido para Preguntas de Preguntas y Respuestas. Si no hay ninguno seleccionado, se muestran todos.

>[!NOTE]
>
>Si solo se selecciona el estado No respondida, el moderador verá todo el contenido (para todos los tipos de contenido) excepto las preguntas respondidas. Es así porque la propiedad responsable de la pregunta respondida no existe en el caso de preguntas no respondidas y otro contenido como tema del foro, artículo del blog o comentarios.

![estados](assets/statuses.png)

#### Indicación {#flagging}

El marcado limita el UGC referenciado mostrado a las publicaciones que están marcadas u ocultas.

Una vez marcado un fragmento de contenido, permanece marcado hasta que se desmarca ese único fragmento de contenido seleccionando una vez más el botón **Marcar **nuevamente. Tenga en cuenta que no hay niveles de señalización, como importante o de seguimiento.

![chlimage_1-216](assets/chlimage_1-216.png)

#### Miembros {#members}

Los miembros limitan el UGC referenciado que se muestra en UGC publicado por el nombre del miembro introducido.

![chlimage_1-217](assets/chlimage_1-217.png)

#### Enviado en el último {#posted-in-the-last}

Publicado en Última limita el UGC referenciado que se muestra a las publicaciones realizadas en la última hora, día, semana, mes o año.

![chlimage_1-218](assets/chlimage_1-218.png)

#### Opinión {#sentiment}

[La opinión](/help/communities/moderate-ugc.md#sentiment) limita la UGC referenciada mostrada a las publicaciones con un valor de opinión positivo, negativo o neutro.

![chlimage_1-219](assets/chlimage_1-219.png)

## Custom Filters {#custom-filters}

Aparte de los filtros predeterminados en [Filtro de carril](/help/communities/moderation.md#ootbfilters), se pueden añadir filtros personalizados adicionales en los metadatos a la interfaz de usuario de moderación. Los desarrolladores pueden utilizar el código de muestra en Github para ampliar los filtros de la interfaz de usuario de moderación existentes.

![custom-tag-filter](assets/custom-tag-filter.png)

El proyecto [de](https://github.com/Adobe-Marketing-Cloud/aem-communities-extensions/tree/master/aem-communities-moderation-filter) ejemplo de Github implementa el filtro Tag para filtrar la lista UGC en función de si las etiquetas específicas se aplican al contenido generado por el usuario. Puede seguir el código de muestra y crear filtros análogos para otros campos de metadatos UGC similares.

Para instalar el ejemplo para el filtro Etiquetas:

1. Abra el administrador de paquetes en la instancia de AEM Author ([https://[aem-author]:4502/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp)) y AEM Publish ([https://[aem-publish]:4503/crx/packmgr/index.jsp](https://aem65-communities-demo.corp.adobe.com:4502/crx/packmgr/index.jsp)).
1. Cree el paquete `com.adobe.social.sample.moderation.filter.ui.apps-1.0-SNAPSHOT.zip` a partir del código de Github, e instale y habilite lo mismo.
1. Abra la consola de paquetes en la instancia de AEM Author ( `https://[aem-author]:4502/system/console/bundles`) y en la instancia de AEM Publish ( `https://[aem-publish]:4503/system/console/bundles`).
1. Compile el paquete ` [com](https://sample-moderation-filter.com/).adobe.social.sample.moderation.filter.core-1.0-SNAPSHOT.jar` desde Github, e instale y active lo mismo.
1. Vaya al nodo **/apps/social/moderation/facets** de AEM Author ([https://[aem-author]:4502/crx/de/index.jsp#/apps/social/moderation/facets](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets)) y AEM Publish ([https://[aem-publish]:4502/crx/de/index.jsp#/apps/social/moderation/facets](https://aem65-communities-demo.corp.adobe.com:4502/crx/de/index.jsp#/apps/social/moderation/facets)).
1. Agregue **comunidades de usuarios técnicos-utilidades-reader** con `jcr:read` permisos.

Para exponer los filtros personalizados en sitios de comunidad existentes:

1. Editar `Clientlibs` la página de moderación existente `/content/we-retail/us/en/community/moderation/shell3/jcr:content/head/clientlibs.`

   * Agregar nueva categoría `cq.social.hbs.moderation.v2.`

1. Ir a `/content/we-retail/us/en/community/moderation/shell3/jcr:content/rails/searchWell/items/filters.`

   * Establecer en nuevo componente `sling:resourceType = social/moderation/v2/filters.`

1. Ir a `/content/we-retail/us/en/community/moderation/shell3/jcr:content/views/content/items/modcontainer`.

   * Se establece en un nuevo componente `sling:resourceType = social/moderation/v2/modcontainer`.

## Acciones de moderación {#moderation-actions}

[Las acciones](/help/communities/moderate-ugc.md#moderation-actions) de moderación se pueden realizar en una o varias selecciones realizadas en el área de contenido o al visualizar los detalles del contenido.

Para moderar las publicaciones de forma masiva, en el área de contenido, haga clic en el icono Seleccionar ( ![selecticono](assets/selecticon.png)) de una publicación, que aparece al pasar el ratón sobre ella (escritorio) o al pulsar y mantener un dedo en la publicación (móvil). Al hacer esto, se entra en el modo de selección múltiple y ahora puede seleccionar las publicaciones subsiguientes que se van a moderar de forma masiva haciendo clic en ellas. Utilice los botones que se muestran en la barra de herramientas para realizar acciones de moderación en los anuncios seleccionados. Todas las acciones solicitarán confirmación.

Para moderar una sola publicación en el área de contenido, pase el ratón sobre ella (escritorio) o mantenga presionado el dedo sobre la publicación (móvil) para que aparezcan los botones en la publicación. Cuando se trabaja con un solo detalle de contenido, solo una acción de eliminación solicitará confirmación.

### Moderación de varias publicaciones {#moderating-multiple-posts}

Para acceder al modo de selección masiva, haga clic en el icono `Select` de una publicación:

![select-icon](assets/select-icon.png)

Para salir del modo de selección masiva, seleccione el icono Cancelar (x) en la barra de herramientas:

Las acciones de moderación que se pueden realizar en varias publicaciones son:

* Denegar
* Eliminar
* Cerrar/volver a abrir los anuncios

Los iconos que permiten estas acciones solo aparecen en la barra de herramientas cuando se seleccionan varios anuncios.

![bulkmoder](assets/bulkmoderate.png)

### Moderación de una sola publicación {#moderating-a-single-post}

En el modo de selección única, es posible

* para ver los detalles del usuario, seleccione su nombre
* ver la publicación en contexto seleccionando el vínculo a la publicación
* [respuesta](#reply)
* [Permitir](#allow)
* [Denegar](#deny)
* [Eliminar](#delete)
* [Cerrar](#close)
* ver historial [de moderación](#moderation-history)
* [Ver detalles](#viewdetails)

Presente en la vista de tarjeta encima de los iconos de acción de moderación es el texto de la publicación y debajo hay datos que indican

* si tiene respuestas, y en caso afirmativo, precedidas del número de respuestas
* si se ha marcado
* si se ha aprobado
* cuándo se publicó el UGC

![singeselectmode](assets/singleselectmode.png)

#### respuesta {#reply}

![chlimage_1-220](assets/chlimage_1-220.png)

Al trabajar con un solo anuncio, aparecerá un icono de respuesta si el tipo UGC admite respuestas y está configurado para permitir respuestas.

#### Permitir {#allow}

![chlimage_1-221](assets/chlimage_1-221.png)

Al trabajar con un solo anuncio, el icono Permitir aparecerá cuando el anuncio se haya marcado o denegado. Si se marca, al seleccionar Permitir se borrarán todos los indicadores.

#### Denegar {#deny}

![chlimage_1-222](assets/chlimage_1-222.png)

La acción de moderación **Denegar **solo está disponible para contenido moderado y no aparece en contenido no moderado excepto en modo de selección múltiple.

El contenido que no se modera siempre se aprueba.

El contenido que se modera inicialmente entra en un estado Pendiente y luego se puede modificar para aprobarlo o denegarlo.

El contenido que deja el estado pendiente nunca puede volver a un estado pendiente. El contenido marcado como aprobado o denegado se puede cambiar a otro estado en cualquier momento.

#### Eliminar {#delete}

![chlimage_1-223](assets/chlimage_1-223.png)

En el modo de selección única o masiva, puede seleccionar elementos y eliminarlos. La acción de eliminar resulta en un cuadro de diálogo de confirmación. Una vez eliminados, esos elementos desaparecen inmediatamente del área de contenido. **Una vez que se elimina UGC, se elimina permanentemente del repositorio y no se puede recuperar posteriormente.**

#### Cerrar {#close}

![chlimage_1-224](assets/chlimage_1-224.png)

Al trabajar con un solo anuncio, aparecerá un icono de cierre si el tipo UGC admite la capacidad de evitar más anuncios para ese recurso.

#### Historial de moderación {#moderation-history}

![chlimage_1-225](assets/chlimage_1-225.png)

Al trabajar con una sola publicación, aparecerá un icono Historial de moderación al pasar el ratón por encima. Al seleccionar el icono, se mostrará un panel que contiene un historial de acciones realizadas con respecto al anuncio de UGC.

Para volver a la visualización del área de contenido de varias publicaciones UGC, seleccione la X en la esquina superior derecha del panel de detalles de la vista.

Por ejemplo :

![chlimage_1-226](assets/chlimage_1-226.png)

#### Ver detalles {#view-detail}

![chlimage_1-227](assets/chlimage_1-227.png)

Al trabajar con una sola publicación, se pueden ver más detalles abriendo el UGC en modo detallado.

Para ello, pase el ratón sobre el anuncio para mostrar el icono y `View Detail` selecciónelo para mostrar un panel con más detalles del anuncio.

Para volver a la visualización del área de contenido de varias publicaciones UGC, seleccione la X en la esquina superior derecha del panel de detalles de la vista.

Por ejemplo :

![chlimage_1-228](assets/chlimage_1-228.png)

