---
title: Etiquetado del contenido generado por el usuario
seo-title: Tagging User Generated Content
description: El etiquetado del contenido generado por el usuario (UGC) es la forma en que los miembros de la comunidad pueden ayudar a otros miembros a buscar contenido
seo-description: Tagging of user generated content (UGC) is how community members can help other members search for content
uuid: ce125d7c-6fc1-44c7-9f67-eca6f599d8e3
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 1cc8ce66-2c03-44e4-9ddd-8d6944d85c99
role: Admin
exl-id: 1ecb41e5-c959-4380-a5c7-df9fc3a7703a
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 3%

---

# Etiquetado del contenido generado por el usuario {#tagging-user-generated-content}

## Información general {#overview}

El etiquetado del contenido generado por el usuario (UGC) es el medio por el cual los miembros de la comunidad pueden ayudar a otros miembros a buscar contenido.

Normalmente, las etiquetas las aplican autores y administradores en el entorno de creación. El etiquetado de UGC es único, ya que los miembros de la comunidad aplican etiquetas UGC en el entorno de publicación.

Las áreas de nombres y taxonomías de etiquetas son las mismas para ambas aplicaciones.

## Características de Communities {#communities-features}

Las funciones de AEM Communities que se pueden configurar para permitir el etiquetado son las siguientes:

* [Blog](blog-feature.md)
* [Calendario](calendar.md)
* [Biblioteca de archivos](file-library.md)
* [Foro](forum.md#configuretheaddedforum)
* [Preguntas y respuestas](working-with-qna.md)

## Administración de etiquetas {#administering-tags}

Consulte [Administración de etiquetas](../../help/sites-administering/tags.md#tagging-console) para crear y administrar áreas de nombres y taxonomías de etiquetas.

Consulte [Tag Essentials](tag.md) para obtener información del desarrollador.

Consulte [Uso de Social Tag Cloud](tagcloud.md) para añadir un componente Nube de etiquetas social a una página para facilitar la búsqueda de UGC publicados mediante las etiquetas aplicadas.

### Permisos de etiquetas {#tag-permissions}

Los permisos predeterminados están configurados para no permitir que todos los usuarios del entorno de publicación lean las áreas de nombres de etiquetas.

Dado que las etiquetas se aplican a UGC en el entorno de publicación, el permiso de lectura debe habilitarse para que los miembros de la comunidad puedan seleccionar etiquetas para aplicarlas.

Consulte [Configuración de permisos de etiquetas](../../help/sites-administering/tags.md#setting-tag-permissions).

A continuación, se muestra cómo aparece en CRXDE cuando un administrador aplica permisos de lectura a `/etc/tag/discussions` para el grupo `Community Engage Members`.

![tag-permissions](assets/tag-permissions.png)
