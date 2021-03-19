---
title: Creación del etiquetado en una aplicación AEM
seo-title: Creación del etiquetado en una aplicación AEM
description: Trabajo mediante programación con etiquetas o ampliación de etiquetas dentro de una aplicación AEM personalizada
seo-description: Trabajo mediante programación con etiquetas o ampliación de etiquetas dentro de una aplicación AEM personalizada
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
feature: Etiquetado
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---


# Creación del etiquetado en una aplicación AEM{#building-tagging-into-an-aem-application}

Con el fin de trabajar mediante programación con etiquetas o ampliar las etiquetas dentro de una aplicación de AEM personalizada, esta página describe el uso de la variable

* [API de etiquetado](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

que interactúa con el

* [Marco de etiquetado](/help/sites-developing/framework.md)

Para obtener información relacionada con el etiquetado, consulte :

* [Administración de ](/help/sites-administering/tags.md) etiquetas para obtener información sobre cómo crear y administrar las etiquetas, así como sobre las etiquetas de contenido que se han aplicado.
* [Uso de ](/help/sites-authoring/tags.md) etiquetas para obtener información sobre el etiquetado de contenido.

## Información general sobre la API de etiquetado {#overview-of-the-tagging-api}

La implementación del [marco de etiquetado](/help/sites-developing/framework.md) en AEM permite la administración de etiquetas y contenido de etiquetas mediante la API de JCR . TagManager garantiza que las etiquetas introducidas como valores en la propiedad de matriz de cadenas `cq:tags` no se dupliquen, elimina los TagID que apuntan a etiquetas no existentes y actualiza los TagID para etiquetas combinadas o movidas. TagManager utiliza un oyente de observación JCR que revierte cualquier cambio incorrecto. Las clases principales se encuentran en el paquete [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html):

* JcrTagManagerFactory - devuelve una implementación basada en JCR de `TagManager`. Es la implementación de referencia de la API de etiquetado.
* `TagManager` : permite resolver y crear etiquetas por rutas y nombres.
* `Tag` - define el objeto tag .

### Obtención de un TagManager basado en JCR {#getting-a-jcr-based-tagmanager}

Para recuperar una instancia de TagManager, debe tener un JCR `Session` y llamar a `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

En el contexto típico de Sling, también puede adaptarse a un `TagManager` desde el `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recuperación de un objeto Tag {#retrieving-a-tag-object}

Se puede recuperar un `Tag` mediante el `TagManager` resolviendo una etiqueta existente o creando una nueva:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Para la implementación basada en JCR, que asigna `Tags` a JCR `Nodes`, puede utilizar directamente el mecanismo `adaptTo` de Sling si dispone del recurso (por ejemplo, `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Aunque una etiqueta solo se puede convertir *desde *un recurso (no un nodo), una etiqueta se puede convertir *a *un nodo y un recurso :

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>No es posible la adaptación directa de `Node` a `Tag` porque `Node` no implementa el método Sling `Adaptable.adaptTo(Class)`.

### Obtención y configuración de etiquetas {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### Búsqueda de tags {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>El `RangeIterator` válido para usar es:
>
>`com.day.cq.commons.RangeIterator`

### Eliminación de tags {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Duplicación de etiquetas {#replicating-tags}

Es posible utilizar el servicio de replicación ( `Replicator`) con etiquetas porque las etiquetas son de tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## Etiquetado en el lado del cliente {#tagging-on-the-client-side}

`CQ.tagging.TagInputField` es un widget de formulario para introducir etiquetas. Tiene un menú emergente para seleccionar etiquetas existentes, incluye el completado automático y muchas otras funciones. Su xtype es `tags`.

## El recolector de residuos de etiquetas {#the-tag-garbage-collector}

El recolector de residuos de etiquetas es un servicio de fondo que limpia las etiquetas que están ocultas y que no se utilizan. Las etiquetas ocultas y no utilizadas son etiquetas debajo de `/content/cq:tags` que tienen una propiedad `cq:movedTo` y no se utilizan en un nodo de contenido; tienen un recuento de cero. Al utilizar este proceso de eliminación diferido, el nodo de contenido (es decir, la propiedad `cq:tags` ) no tiene que actualizarse como parte de la operación de mover o de combinar. Las referencias de la propiedad `cq:tags` se actualizan automáticamente cuando se actualiza la propiedad `cq:tags`, por ejemplo, a través del cuadro de diálogo de propiedades de la página.

El recolector de residuos de etiquetas se ejecuta de forma predeterminada una vez al día. Esto se puede configurar en:

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## Búsqueda de etiquetas y listado de etiquetas {#tag-search-and-tag-listing}

La búsqueda de etiquetas y la lista de etiquetas funcionan de la siguiente manera:

* La búsqueda de TagID busca las etiquetas que tienen la propiedad `cq:movedTo` establecida en TagID y sigue los `cq:movedTo` TagIDs.

* La búsqueda de Título de etiqueta solo busca las etiquetas que no tienen una propiedad `cq:movedTo`.

## Etiquetas en diferentes idiomas {#tags-in-different-languages}

Como se describe en la documentación para la administración de etiquetas, en la sección [Administración de etiquetas en diferentes idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages), se puede definir una etiqueta `title`en diferentes idiomas. A continuación, se agrega una propiedad que distingue entre idiomas al nodo de etiqueta . Esta propiedad tiene el formato `jcr:title.<locale>`, por ejemplo: `jcr:title.fr` para la traducción al francés. `<locale>` debe ser una cadena de configuración regional ISO en minúscula y utilizar &quot;_&quot; en lugar de &quot;-&quot;, por ejemplo:  `de_ch`.

Cuando se agrega la etiqueta **Animals** a la página **Products**, el valor `stockphotography:animals` se agrega a la propiedad `cq:tags` del nodo /content/geometrixx/en/products/jcr:content. Se hace referencia a la traducción desde el nodo tag .

La API del lado del servidor ha localizado los métodos relacionados con `title`:

* [com.day.cq.tagging.Tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(Configuración regional)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(Configuración regional)
   * getTitlePath(configuración regional)

* [com.day.cq.tagging.TagManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, configuración regional)
   * createTagByTitle(String tagTitlePath, configuración regional)
   * resolveByTitle(String tagTitlePath, configuración regional)

En AEM, el idioma se puede obtener desde el idioma de la página o desde el idioma del usuario:

* para recuperar el idioma de la página en un JSP:

   * `currentPage.getLanguage(false)`

* para recuperar el idioma del usuario en un JSP:

   * `slingRequest.getLocale()`

`currentPage` y  `slingRequest` están disponibles en un JSP a través de la  [&lt;cq:definedobjects>](/help/sites-developing/taglib.md) etiqueta .

Para el etiquetado, la localización depende del contexto, ya que la etiqueta `titles`se puede mostrar en el idioma de la página, en el idioma del usuario o en cualquier otro idioma.

### Adición de un nuevo idioma al cuadro de diálogo Editar etiqueta {#adding-a-new-language-to-the-edit-tag-dialog}

El siguiente procedimiento describe cómo añadir un nuevo idioma (finés) al cuadro de diálogo **Tag Edit**:

1. En **CRXDE**, edite la propiedad de varios valores `languages` del nodo `/content/cq:tags`.

1. Añada `fi_fi`, que representa la configuración regional finlandesa, y guarde los cambios.

El nuevo idioma (finés) ya está disponible en el cuadro de diálogo de etiquetas de las propiedades de página y en el cuadro de diálogo **Editar etiqueta** al editar una etiqueta en la consola **Etiquetado**.

>[!NOTE]
>
>El nuevo idioma debe ser uno de los idiomas AEM reconocidos, es decir, debe estar disponible como nodo debajo de `/libs/wcm/core/resources/languages`.

