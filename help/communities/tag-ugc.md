---
title: Etiquetado del contenido generado por el usuario
seo-title: Etiquetado del contenido generado por el usuario
description: El etiquetado del contenido generado por el usuario (UGC) es la forma en que los miembros de la comunidad pueden ayudar a otros miembros a buscar contenido
seo-description: El etiquetado del contenido generado por el usuario (UGC) es la forma en que los miembros de la comunidad pueden ayudar a otros miembros a buscar contenido
uuid: ce125d7c-6fc1-44c7-9f67-eca6f599d8e3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1cc8ce66-2c03-44e4-9ddd-8d6944d85c99
role: Administrador
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 4%

---


# Etiquetado de contenido generado por el usuario {#tagging-user-generated-content}

## Información general {#overview}

El etiquetado del contenido generado por el usuario (UGC) es el modo en que los miembros de la comunidad pueden ayudar a otros miembros a buscar contenido.

Normalmente, los autores y administradores aplican las etiquetas en el entorno de creación. Etiquetar UGC es único en el sentido de que los miembros de la comunidad aplican las etiquetas UGC en el entorno de publicación.

Los espacios de nombres y las taxonomías de etiquetas son los mismos para ambas aplicaciones.

## Funciones de Communities {#communities-features}

Las funciones de AEM Communities que se pueden configurar para permitir el etiquetado son:

* [Blog](blog-feature.md)
* [Calendario](calendar.md)
* [Biblioteca de archivos](file-library.md)
* [Foro](forum.md#configuretheaddedforum)
* [Preguntas y respuestas](working-with-qna.md)

## Administración de etiquetas {#administering-tags}

Consulte [Administración de etiquetas](../../help/sites-administering/tags.md#tagging-console) para crear y administrar espacios de nombres y taxonomías de etiquetas.

Consulte [Tag Essentials](tag.md) para obtener información sobre el desarrollador.

Consulte [Uso de Social Tag Cloud](tagcloud.md) para agregar un componente de Social Tag Cloud a una página para facilitar la búsqueda de UGC publicado con las etiquetas aplicadas.

### Permisos de etiqueta {#tag-permissions}

Los permisos predeterminados se establecen para que todos los usuarios del entorno de publicación no puedan leer los espacios de nombres de etiquetas.

Dado que las etiquetas se aplican a UGC en el entorno de publicación, el permiso de lectura debe estar habilitado para los miembros de la comunidad para que puedan seleccionar las etiquetas que desee aplicar.

Consulte [Configuración de permisos de etiquetas](../../help/sites-administering/tags.md#setting-tag-permissions).

A continuación se muestra cómo aparece en CRXDE cuando un administrador aplica permisos de lectura a `/etc/tag/discussions` para el grupo `Community Engage Members`.

![tag-permissions](assets/tag-permissions.png)

