---
title: Etiquetado de recursos de habilitación
seo-title: Tagging Enablement Resources
description: El etiquetado de los recursos de habilitación permite filtrar los recursos y las rutas de aprendizaje a medida que los miembros navegan por los catálogos
seo-description: Tagging of enablement resources allows for filtering of resources and learning paths as members browse catalogs
uuid: daf8a4f4-486b-498c-99e9-d1533a830e64
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c012d639-c6e6-4f73-bbd8-78a4baa38c17
role: Admin
exl-id: ce58c8e9-8b4a-43fb-a108-ed2ac40268c7
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# Etiquetado de recursos de habilitación {#tagging-enablement-resources}

## Información general {#overview}

El etiquetado de los recursos de habilitación permite filtrar los recursos y las rutas de aprendizaje a medida que los miembros navegan [catálogos](functions.md#catalog-function).

Esencialmente:

* [Crear un espacio de nombres de etiqueta](../../help/sites-administering/tags.md#creating-a-namespace) para cada catálogo

   * [Definir permisos de etiquetas](../../help/sites-administering/tags.md#setting-tag-permissions)
   * Solo para miembros de la comunidad (comunidad cerrada)

      * Permitir acceso de lectura para la variable [grupo de miembros del sitio de la comunidad](users.md#publish-group-roles)
   * Para cualquier visitante del sitio, ya sea que haya iniciado sesión o que sea anónimo (comunidad abierta)

      * Permitir acceso de lectura para la variable `Everyone` grupo
   * [Publicación de las etiquetas](../../help/sites-administering/tags.md#publishing-tags)



* [Definir el ámbito de las etiquetas de un sitio de comunidad](sites-console.md#tagging)

   * [Configurar los catálogos que existen en la estructura del sitio](functions.md#catalog-function)

      * Puede añadir etiquetas a la instancia de catálogo para controlar la lista de etiquetas presentadas en los filtros de interfaz de usuario.
      * Puede agregar [filtros previos](catalog-developer-essentials.md#pre-filters), para restringir los recursos incluidos de un catálogo.

* [Publicar el sitio de la comunidad](sites-console.md#publishing-the-site)
* [Aplicación de etiquetas a los recursos de habilitación](resources.md#create-a-resource) por lo que se pueden filtrar categóricamente
* [Publicación de los recursos de habilitación](resources.md#publish)

## Etiquetas de sitios de la comunidad {#community-site-tags}

Al crear o editar un sitio de comunidad, la variable [Configuración de etiquetado](sites-console.md#tagging) define el ámbito de las etiquetas disponibles para las características del sitio seleccionando un subconjunto de áreas de nombres de etiquetas existentes.

Aunque las etiquetas se pueden crear y agregar al sitio de la comunidad en cualquier momento, se recomienda diseñar una taxonomía de antemano, similar a diseñar una base de datos. Consulte [Uso de etiquetas](../../help/sites-authoring/tags.md).

Cuando más tarde se agregan etiquetas a un sitio de comunidad existente, es necesario guardar la edición antes de poder agregar la nueva etiqueta a una función de catálogo en la estructura del sitio.

Para un sitio de la comunidad, una vez publicado el sitio y las etiquetas publicadas, es necesario permitir el acceso de lectura a los miembros de la comunidad. Consulte [Configuración de permisos de etiquetas](../../help/sites-administering/tags.md#setting-tag-permissions).

A continuación se muestra cómo aparece en CRXDE cuando un administrador aplica permisos de lectura a `/etc/tags/ski-catalog` para el grupo `Community Enable Members`.

![site-tags](assets/site-tags.png)

## Espacios de nombres de etiquetas del catálogo {#catalog-tag-namespaces}

La función de catálogo utiliza etiquetas para definirse. Al configurar la función de catálogo en un sitio de comunidad, el conjunto de áreas de nombres de etiquetas entre las que elegir se define mediante el ámbito de los espacios de nombres de etiquetas definido para el sitio de comunidad.

La función Catálogo incluye una configuración de etiqueta que define las etiquetas que aparecen en la interfaz de usuario del filtro para el catálogo. La configuración &quot;Todos los espacios de nombres&quot; hace referencia al ámbito de los espacios de nombres de etiquetas seleccionados para el sitio de la comunidad.

![catalog-namespace](assets/catalog-namespace.png)

## Aplicación de etiquetas a recursos de habilitación {#applying-tags-to-enablement-resources}

Los recursos de habilitación y las rutas de aprendizaje aparecerán en todo el catálogo cuando `Show in Catalog` está activada. Añadir etiquetas a los recursos y a las rutas de aprendizaje permitirá el prefiltrado en catálogos específicos, así como el filtrado en la interfaz de usuario del catálogo.

La restricción de los recursos de habilitación y las rutas de aprendizaje a catálogos específicos se logra mediante la creación de [filtros previos](catalog-developer-essentials.md#pre-filters).

La interfaz de usuario del catálogo permite a los visitantes aplicar un filtro de etiquetas a la lista de recursos y rutas de aprendizaje que aparecen en dicho catálogo.

El administrador que aplique las etiquetas a los recursos de habilitación debe tener en cuenta las áreas de nombres de etiquetas asociadas con los catálogos, así como la taxonomía para seleccionar una subetiqueta para una categorización más refinada.

Por ejemplo, si una `ski-catalog` se crearon y se establecieron en un catálogo denominado `Ski Catalog`, puede tener dos etiquetas secundarias: `lesson-1` y `lesson-2`.

Por lo tanto, cualquier recurso de habilitación etiquetado con uno de los siguientes elementos:

* ski-catalog:lección-1
* ski-catalog:lección-2

aparecerá en `Ski Catalog` después de publicar el recurso de habilitación.

![basic-info](assets/applytags-basicinfo.png)

## Visualización del catálogo al publicar {#viewing-catalog-on-publish}

Una vez que todo se ha configurado desde el entorno de creación y se ha publicado, la experiencia de utilizar el catálogo para encontrar recursos de habilitación se puede experimentar en el entorno de publicación.

Si no aparece ningún área de nombres de etiquetas en la lista desplegable, asegúrese de que los permisos se hayan establecido correctamente en el entorno de publicación.

Si se agregaron áreas de nombres de etiquetas que faltan, asegúrese de que las etiquetas y el sitio se volvieron a publicar.

Si no aparecen recursos de habilitación después de seleccionar una etiqueta al ver el catálogo, asegúrese de que haya una etiqueta del área de nombres del catálogo aplicada al recurso de habilitación.

![view-catalog](assets/viewcatalog.png)
