---
title: Etiquetado de recursos de habilitación
seo-title: Etiquetado de recursos de habilitación
description: El etiquetado de los recursos de habilitación permite filtrar los recursos y las rutas de aprendizaje a medida que los miembros exploran los catálogos
seo-description: El etiquetado de los recursos de habilitación permite filtrar los recursos y las rutas de aprendizaje a medida que los miembros exploran los catálogos
uuid: daf8a4f4-486b-498c-99e9-d1533a830e64
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: c012d639-c6e6-4f73-bbd8-78a4baa38c17
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Etiquetado de recursos de habilitación {#tagging-enablement-resources}

## Información general {#overview}

El etiquetado de los recursos de habilitación permite filtrar los recursos y las rutas de aprendizaje a medida que los miembros exploran [los catálogos](functions.md#catalog-function).

Esencialmente:

* [Creación de un espacio de nombres](../../help/sites-administering/tags.md#creating-a-namespace) de etiquetas para cada catálogo

   * [Definir permisos de etiquetas](../../help/sites-administering/tags.md#setting-tag-permissions)

      * Solo para miembros de la comunidad (comunidad cerrada)

         * Permitir acceso de lectura para el grupo de miembros del sitio de [comunidad](users.md#publish-group-roles)
      * Para cualquier visitante del sitio, ya sea que haya iniciado sesión o sea anónimo (comunidad abierta)

         * Permitir acceso de lectura para el `Everyone`grupo
   * [Publicación de las etiquetas](../../help/sites-administering/tags.md#publishing-tags)



* [Definir el alcance de las etiquetas de un sitio de comunidad](sites-console.md#tagging)

   * [Configurar los catálogos que existen en la estructura del sitio](functions.md#catalog-function)

      * Puede agregar etiquetas a la instancia de catálogo para controlar la lista de etiquetas presentadas en los filtros de interfaz de usuario
      * Puede agregar [prefiltros](catalog-developer-essentials.md#pre-filters)para restringir los recursos incluidos en un catálogo

* [Publicar el sitio de la comunidad](sites-console.md#publishing-the-site)
* [Aplicar etiquetas a los recursos](resources.md#create-a-resource) de habilitación para que se puedan filtrar categóricamente
* [Publicación de los recursos de habilitación](resources.md#publish)

## Etiquetas del sitio de la comunidad {#community-site-tags}

Al crear o editar un sitio de comunidad, la opción [Etiquetado](sites-console.md#tagging) establece el alcance de las etiquetas disponibles para las funciones del sitio seleccionando un subconjunto de espacios de nombres de etiquetas existentes.

Aunque las etiquetas se pueden crear y agregar al sitio de la comunidad en cualquier momento, se recomienda diseñar una taxonomía de antemano, de manera similar a diseñar una base de datos. Consulte [Uso de etiquetas](../../help/sites-authoring/tags.md).

Cuando más tarde se agregan etiquetas a un sitio de comunidad existente, es necesario guardar la edición antes de poder agregar la nueva etiqueta a una función de catálogo en la estructura del sitio.

Para un sitio de comunidad, una vez que se haya publicado el sitio y las etiquetas, es necesario habilitar el acceso de lectura para los miembros de la comunidad. Consulte [Configuración de permisos](../../help/sites-administering/tags.md#setting-tag-permissions)de etiquetas.

A continuación se muestra cómo aparece en CRXDE cuando un administrador aplica permisos de lectura a `/etc/tags/ski-catalog` para el grupo `Community Enable Members`.

![chlimage_1-420](assets/chlimage_1-420.png)

## Espacios de nombres de etiquetas de catálogo {#catalog-tag-namespaces}

La función de catálogo utiliza etiquetas para definirse. Al configurar la función de catálogo en un sitio de comunidad, el conjunto de espacios de nombres de etiquetas para elegir se define mediante el ámbito de los espacios de nombres de etiquetas establecidos para el sitio de comunidad.

La función Catálogo incluye un ajuste de etiqueta que define las etiquetas que aparecen en la interfaz de usuario del filtro para el catálogo. La configuración &quot;Todos los espacios de nombres&quot; hace referencia al ámbito de los espacios de nombres de etiquetas seleccionados para el sitio de comunidad.

![chlimage_1-421](assets/chlimage_1-421.png)

## Aplicación de etiquetas a los recursos de habilitación {#applying-tags-to-enablement-resources}

Los recursos de habilitación y las rutas de aprendizaje aparecerán en todo el catálogo cuando `Show in Catalog` se marque. La adición de etiquetas a recursos y rutas de aprendizaje permitirá realizar un filtrado previo en catálogos específicos, así como filtrar en la interfaz de usuario del catálogo.

La restricción de recursos de habilitación y rutas de aprendizaje a catálogos específicos se logra mediante la creación de [prefiltros](catalog-developer-essentials.md#pre-filters).

La interfaz de usuario del catálogo permite a los visitantes aplicar un filtro de etiquetas a la lista de recursos y rutas de aprendizaje que aparecen en ese catálogo.

El administrador que aplique las etiquetas a los recursos de habilitación debe tener en cuenta los espacios de nombres de etiquetas asociados a los catálogos, así como la taxonomía para seleccionar una subetiqueta para una categorización más refinada.

Por ejemplo, si se crea un `ski-catalog` espacio de nombres y se establece en un catálogo denominado `Ski Catalog`, puede tener dos etiquetas secundarias: `lesson-1` y `lesson-2`.

Por lo tanto, cualquier recurso de habilitación etiquetado con uno de los siguientes elementos:

* ski-catalog:
* ski-catálogo:lección-1
* ski-catálogo:lección-2

aparecerá en `Ski Catalog` una vez que se haya publicado el recurso de habilitación.

![chlimage_1-422](assets/chlimage_1-422.png)

## Visualización del catálogo al publicar {#viewing-catalog-on-publish}

Una vez que todo se haya configurado desde el entorno de creación y se haya publicado, la experiencia de utilizar el catálogo para encontrar recursos de habilitación se puede experimentar en el entorno de publicación.

Si no aparece ningún espacio de nombres de etiquetas en la lista desplegable, asegúrese de que los permisos se han establecido correctamente en el entorno de publicación.

Si se han agregado espacios de nombres de etiquetas y faltan, asegúrese de que las etiquetas y el sitio se han vuelto a publicar.

Si no aparece ningún recurso de habilitación después de seleccionar una etiqueta al ver el catálogo, asegúrese de que haya una etiqueta del espacio de nombres del catálogo aplicada al recurso de habilitación.

![chlimage_1-423](assets/chlimage_1-423.png)

