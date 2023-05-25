---
title: AEM Creación de etiquetas en una aplicación de
seo-title: Building Tagging into an AEM Application
description: AEM Trabajar mediante programación con etiquetas o ampliar etiquetas dentro de una aplicación de personalizada
seo-description: Programmatically work with tags or extending tags within a custom AEM application
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
feature: Tagging
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
source-git-commit: 325af649564d93beedfc762a8f5beacec47b1641
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 0%

---

# AEM Creación de etiquetas en una aplicación de{#building-tagging-into-an-aem-application}

AEM Para trabajar mediante programación con etiquetas o ampliar etiquetas dentro de una aplicación personalizada, esta página describe el uso de la variable

* [API de etiquetado](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/package-summary.html)

Que interactúa con el

* [Marco de etiquetado](/help/sites-developing/framework.md)

Para obtener información relacionada con el etiquetado, consulte:

* [Administración de etiquetas](/help/sites-administering/tags.md) para obtener información sobre cómo crear y administrar etiquetas, y a qué etiquetas de contenido se han aplicado.
* [Uso de etiquetas](/help/sites-authoring/tags.md) para obtener información sobre cómo etiquetar contenido.

## Información general sobre la API de etiquetado {#overview-of-the-tagging-api}

La implementación de la [marco de etiquetado](/help/sites-developing/framework.md) AEM en permite la administración de etiquetas y contenido de etiquetas mediante la API de JCR. TagManager garantiza que las etiquetas introducidas como valores en la `cq:tags` Las propiedades de matriz de cadenas no están duplicadas, elimina los TagID que apuntan a etiquetas no existentes y actualiza los TagID para etiquetas movidas o combinadas. TagManager utiliza un detector de observación JCR que revierte cualquier cambio incorrecto. Las clases principales se encuentran en la [com.day.cq.tagging](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/package-summary.html) paquete:

* JcrTagManagerFactory: devuelve una implementación basada en JCR de un `TagManager`. Es la implementación de referencia de la API de etiquetado.
* `TagManager` : permite resolver y crear etiquetas por rutas y nombres.
* `Tag` : define el objeto de etiqueta.

### Obtener un TagManager basado en JCR {#getting-a-jcr-based-tagmanager}

Para recuperar una instancia de TagManager, debe tener un JCR `Session` y para llamar a `getTagManager(Session)`:

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

A `Tag` se puede recuperar mediante la variable `TagManager`, ya sea resolviendo una etiqueta existente o creando una:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Para la implementación basada en JCR, que asigna `Tags` en JCR `Nodes`, puede utilizar directamente el de Sling `adaptTo` mecanismo si tiene el recurso (por ejemplo, como `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Aunque una etiqueta solo se puede convertir *de *un recurso (no un nodo), una etiqueta se puede convertir *a *un nodo y un recurso :

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Adaptación directa desde `Node` hasta `Tag` no es posible, ya que `Node` no implementa el Sling `Adaptable.adaptTo(Class)` método.

### Obtención y configuración de etiquetas {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### Búsqueda de etiquetas {#searching-for-tags}

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
>El válido `RangeIterator` para usar es:
>
>`com.day.cq.commons.RangeIterator`

### Eliminación de etiquetas {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Duplicación de etiquetas {#replicating-tags}

Es posible utilizar el servicio de replicación ( `Replicator`) con etiquetas porque son del tipo `nt:hierarchyNode`:

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## Etiquetado en el lado del cliente {#tagging-on-the-client-side}

El widget del formulario `CQ.tagging.TagInputField` es para introducir etiquetas. Tiene un menú emergente para seleccionar entre las etiquetas existentes, incluye finalización automática y muchas otras funciones. Su xtype es `tags`.

## El recolector de basura de etiquetas {#the-tag-garbage-collector}

El recolector de etiquetas es un servicio en segundo plano que limpia las etiquetas ocultas y no utilizadas. Las etiquetas ocultas y no utilizadas son las siguientes `/content/cq:tags` que tienen un `cq:movedTo` y no se utilizan en un nodo de contenido; tienen un recuento de cero. Al utilizar este proceso de eliminación diferida, el nodo de contenido (es decir, el `cq:tags` ) no tiene que actualizarse como parte de la operación de movimiento o combinación. Las referencias en la variable `cq:tags` Las propiedades de se actualizan automáticamente cuando `cq:tags` La propiedad de se actualiza, por ejemplo, a través del cuadro de diálogo Propiedades de página.

El recolector de elementos no utilizados se ejecuta de forma predeterminada una vez al día. Puede configurarlo en:

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## Búsqueda de etiquetas y Listado de etiquetas {#tag-search-and-tag-listing}

La búsqueda de etiquetas y la lista de etiquetas funcionan de la siguiente manera:

* La búsqueda de TagID busca las etiquetas que tienen la propiedad `cq:movedTo` se establece en TagID y sigue el `cq:movedTo` ID de etiqueta.

* La búsqueda de Título de etiqueta solo busca las etiquetas que no tienen un `cq:movedTo` propiedad.

## Etiquetas en diferentes idiomas {#tags-in-different-languages}

Como se describe en la documentación para la administración de etiquetas, en la sección [Administración de etiquetas en diferentes idiomas](/help/sites-administering/tags.md#managing-tags-in-different-languages), una etiqueta `title`puede definirse en diferentes idiomas. A continuación, se agrega una propiedad sensible al idioma al nodo de etiquetas. Esta propiedad tiene el formato `jcr:title.<locale>`, por ejemplo, `jcr:title.fr` para la traducción al francés. El `<locale>` debe ser una cadena de configuración regional ISO en minúsculas y utilizar &quot;_&quot; en lugar de &quot;-&quot;, por ejemplo: `de_ch`.

Si la variable **Animales** se agrega a la etiqueta **Productos** página, el valor `stockphotography:animals` se añade a la propiedad `cq:tags` del nodo /content/geometrixx/en/products/jcr:content. Se hace referencia a la traducción desde el nodo de etiqueta.

La API del lado del servidor se ha localizado `title`Métodos relacionados con:

* [com.day.cq.tagging.Tag](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(Configuración regional)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(Configuración regional)
   * getTitlePath(Locale locale)

* [com.day.cq.tagging.TagManager](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, Configuración regional)
   * createTagByTitle(String tagTitlePath, Configuración regional)
   * resolveByTitle(String tagTitlePath, Configuración regional)

AEM En la práctica, el idioma se puede obtener en el idioma de la página o en el idioma del usuario:

* para recuperar el idioma de la página en un JSP:

   * `currentPage.getLanguage(false)`

* para recuperar el idioma del usuario en un JSP:

   * `slingRequest.getLocale()`

El `currentPage` y `slingRequest` están disponibles en un JSP a través del [&lt;cq:definedobjects>](/help/sites-developing/taglib.md) etiqueta.

Para el etiquetado, la localización depende del contexto como etiqueta `titles`puede mostrarse en el idioma de la página, en el idioma del usuario o en cualquier otro idioma.

### Adición de un nuevo idioma al cuadro de diálogo Editar etiqueta {#adding-a-new-language-to-the-edit-tag-dialog}

El siguiente procedimiento describe cómo agregar un idioma (finés) al **Edición de etiquetas** diálogo:

1. Entrada **CRXDE**, edite la propiedad de varios valores `languages` del nodo `/content/cq:tags`.

1. Añadir `fi_fi` - que representa la configuración regional finlandesa - y guarde los cambios.

El nuevo idioma (finés) ya está disponible en el cuadro de diálogo de etiquetas de las propiedades de página y en el **Editar etiqueta** diálogo al editar una etiqueta en la **Etiquetado** consola.

>[!NOTE]
>
>AEM El nuevo idioma debe ser uno de los idiomas reconocidos por la comunidad de idiomas de los que se dispone en la. Es decir, debe estar disponible como nodo debajo de `/libs/wcm/core/resources/languages`.

>[!CAUTION]
>
>La instalación de un Service Pack restablece la propiedad de idiomas del nodo /content/cq:tags de forma predeterminada. Por lo tanto, es necesario agregarlo desde las propiedades antes de la instalación.
