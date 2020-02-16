---
title: Creación del etiquetado en una aplicación AEM
seo-title: Creación del etiquetado en una aplicación AEM
description: Trabajar mediante programación con etiquetas o ampliar etiquetas dentro de una aplicación personalizada de AEM
seo-description: Trabajar mediante programación con etiquetas o ampliar etiquetas dentro de una aplicación personalizada de AEM
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Creación del etiquetado en una aplicación AEM{#building-tagging-into-an-aem-application}

Para trabajar mediante programación con etiquetas o ampliar etiquetas dentro de una aplicación personalizada de AEM, en esta página se describe el uso de la variable

* [API de etiquetado](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

que interactúa con el

* [Marco de etiquetado](/help/sites-developing/framework.md)

Para obtener información relacionada con el etiquetado, consulte :

* [Administración de etiquetas](/help/sites-administering/tags.md) para obtener información sobre la creación y administración de etiquetas, así como sobre las etiquetas de contenido que se han aplicado.
* [Uso de etiquetas](/help/sites-authoring/tags.md) para obtener información sobre el etiquetado de contenido.

## Información general sobre la API de etiquetado {#overview-of-the-tagging-api}

La implementación del marco [de](/help/sites-developing/framework.md) etiquetado en AEM permite la administración de etiquetas y contenido de etiquetas mediante la API de JCR. TagManager garantiza que las etiquetas introducidas como valores en la propiedad de matriz de `cq:tags` cadenas no se dupliquen, elimina los TagID que apuntan a etiquetas no existentes y actualiza los TagID para etiquetas combinadas o movidas. TagManager utiliza un detector de observación JCR que revierte los cambios incorrectos. Las clases principales se encuentran en el paquete [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) :

* JcrTagManagerFactory: devuelve una implementación basada en JCR de un `TagManager`. Es la implementación de referencia de la API de etiquetado.
* `TagManager` - permite resolver y crear etiquetas por rutas y nombres.
* `Tag` - define el objeto tag.

### Obtención de un TagManager basado en JCR {#getting-a-jcr-based-tagmanager}

Para recuperar una instancia de TagManager, debe tener un JCR `Session` y llamar a `getTagManager(Session)`:

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

En el contexto típico de Sling también puede adaptarse a un `TagManager` de los `ResourceResolver`:

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Recuperación de un objeto Tag {#retrieving-a-tag-object}

Un `Tag` se puede recuperar mediante el `TagManager`, ya sea resolviendo una etiqueta existente o creando una nueva:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Para la implementación basada en JCR, que se asigna `Tags` a JCR `Nodes`, puede utilizar directamente el `adaptTo` mecanismo de Sling si dispone del recurso (por ejemplo, `/etc/tags/default/my/tag`):

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
>No es posible realizar la adaptación directa de `Node` a `Tag` , ya que `Node` no implementa el `Adaptable.adaptTo(Class)` método Sling.

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
>El valor válido `RangeIterator` para usar es:
>
>`com.day.cq.commons.RangeIterator`

### Eliminación de tags {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Replicar etiquetas {#replicating-tags}

Es posible utilizar el servicio de replicación ( `Replicator`) con etiquetas porque las etiquetas son del tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## Etiquetado en el lado del cliente {#tagging-on-the-client-side}

`CQ.tagging.TagInputField` es un widget de formulario para introducir etiquetas. Tiene un menú emergente para seleccionar etiquetas existentes, incluye la finalización automática y muchas otras funciones. Su xtype es `tags`.

## Recopilador de elementos no utilizados de etiquetas {#the-tag-garbage-collector}

El recolector de elementos no utilizados de etiquetas es un servicio de fondo que limpia las etiquetas que están ocultas y no se usan. Las etiquetas ocultas y no utilizadas son las que aparecen debajo `/etc/tags` y que tienen una `cq:movedTo` propiedad y no se utilizan en un nodo de contenido; tienen un recuento de cero. Al utilizar este proceso de eliminación diferido, el nodo de contenido (es decir, la `cq:tags` propiedad) no tiene que actualizarse como parte de la operación de mover o combinar. Las referencias de la propiedad `cq:tags` se actualizan automáticamente cuando se actualiza la `cq:tags` propiedad, por ejemplo, a través del cuadro de diálogo de propiedades de página.

El recolector de elementos no utilizados de etiquetas se ejecuta de forma predeterminada una vez al día. Puede configurarse en:

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## Búsqueda de etiquetas y Lista de etiquetas {#tag-search-and-tag-listing}

La búsqueda de etiquetas y la lista de etiquetas funcionan de la siguiente manera:

* La búsqueda de TagID busca las etiquetas que tienen la propiedad `cq:movedTo` configurada en TagID y sigue los `cq:movedTo` TagID.

* La búsqueda de título de etiqueta solo busca las etiquetas que no tienen una `cq:movedTo` propiedad.

## Tags in Different Languages {#tags-in-different-languages}

Como se describe en la documentación para la administración de etiquetas, en la sección [Administración de etiquetas en distintos idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages), una etiqueta `title`puede definirse en diferentes idiomas. A continuación, se agrega una propiedad que distingue entre lenguajes al nodo de etiquetas. Esta propiedad tiene el formato `jcr:title.<locale>`, por ejemplo `jcr:title.fr` para la traducción al francés. `<locale>` debe ser una cadena de configuración regional ISO en minúscula y utilizar &quot;_&quot; en lugar de &quot;-&quot;, por ejemplo: `de_ch`.

Cuando se agrega la etiqueta **Animals** a la página **Productos** , el valor `stockphotography:animals` se agrega a la propiedad `cq:tags` del nodo /content/geometrixx/en/products/jcr:content. Se hace referencia a la traducción desde el nodo de etiqueta.

La API de servidor tiene métodos `title`relacionados con la localización:

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

`currentPage` y `slingRequest` están disponibles en un JSP mediante la etiqueta [&lt;cq:definedObjects>](/help/sites-developing/taglib.md) .

Para el etiquetado, la localización depende del contexto, ya que la etiqueta se `titles`puede mostrar en el idioma de la página, en el idioma del usuario o en cualquier otro idioma.

### Adición de un nuevo idioma al cuadro de diálogo Editar etiqueta {#adding-a-new-language-to-the-edit-tag-dialog}

El siguiente procedimiento describe cómo agregar un nuevo idioma (finés) al cuadro de diálogo Editar **** etiqueta:

1. En **CRXDE**, edite la propiedad de varios valores `languages` del nodo `/etc/tags`.

1. Agregue `fi_fi` - que representa la configuración regional finlandesa- y guarde los cambios.

El nuevo idioma (finés) ya está disponible en el cuadro de diálogo de etiquetas de las propiedades de página y en el cuadro de diálogo **Editar etiqueta** al editar una etiqueta en la consola **Etiquetado** .

>[!NOTE]
>
>El nuevo idioma debe ser uno de los idiomas reconocidos por AEM, es decir, debe estar disponible como nodo a continuación `/libs/wcm/core/resources/languages`.

