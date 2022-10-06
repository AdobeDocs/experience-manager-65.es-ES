---
title: Elementos esenciales del blog
seo-title: Blog Essentials
description: Información general del blog
seo-description: Blog overview
uuid: 714cf70c-76a0-4be6-9163-a31ac6bd1643
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: eece7b8f-6ccd-4037-8713-0cd36cfd9e73
docset: aem65
exl-id: 51f616e8-4aba-47f6-b948-d5147d84bbb6
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '442'
ht-degree: 2%

---

# Elementos esenciales del blog {#blog-essentials}

Desde AEM 6.1 Communities, un blog es una actividad comunitaria. Los artículos de blog ahora se publican desde el entorno de publicación, donde anteriormente, los artículos de blog solo podían crearse en el entorno de creación y publicarse.

Los artículos de blog pueden ser creados por cualquier miembro de la comunidad, a menos que estén restringidos a miembros privilegiados.

Esta página proporciona la información esencial para trabajar con la función de blog.

>[!NOTE]
>
>La infraestructura subyacente de la función de blog es la función de diario.

## Elementos esenciales para el cliente {#essentials-for-client-side}

La función de blog consta de dos componentes principales que están disponibles añadiendo la variable [Función del blog](/help/communities/functions.md#blog-function) o añadiendo los componentes a una página en modo de edición de autor.

### Blog {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.vote<br /> cq.social.hbs.journal</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/journal/components/hbs/journal/journal.hbs<br /> /libs/social/journal/components/hbs/entry_topic/list-item.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/journal/components/hbs/journal/clientlibs/journal.css</td>
  </tr>
  <tr>
   <td><strong> propiedades</strong></td>
   <td>see <a href="/help/communities/blog-feature.md">Función del blog</a></td>
  </tr>
 </tbody>
</table>

### Barra lateral de blog {#blog-sidebar}

| **resourceType** | social/journal/components/hbs/sidebar |
|---|---|
| [**inclusible**](/help/communities/scf.md#add-or-include-a-communities-component) | No |
| [**clientllibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **plantillas** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **propiedades** | see [Función del blog](/help/communities/blog-feature.md) |

* [Personalizaciones del lado del cliente](/help/communities/client-customize.md)

## Elementos esenciales para el servidor {#essentials-for-server-side}

* [API de blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [Puntos finales de blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](/help/communities/server-customize.md)

### Función Blog {#blog-function}

Una estructura de sitio de la comunidad que incluye el [Función del blog](/help/communities/functions.md#blog-function) se habrá configurado `Blog` y `Blog Sidebar` componentes. La función Blog admite la identificación de un [grupo de usuarios miembro privilegiado](/help/communities/users.md#privileged-members-group).

### Acceso a entradas de blog (UGC) {#accessing-blog-entries-ugc}

UGC debe moderarse utilizando uno de los métodos estándar de moderación.
Consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

A partir del AEM 6.1 Comunidades, se utilizará un [tienda común](/help/communities/working-with-srp.md) para UGC incluye acceso programático a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte :

* [Información general del proveedor de recursos de almacenamiento](/help/communities/srp.md) : introducción y descripción general del uso del repositorio.
* [Elementos esenciales de SRP y UGC](/help/communities/srp-and-ugc.md) - Métodos y ejemplos de utilidad SRP.
* [Acceso a UGC con SRP](/help/communities/accessing-ugc-with-srp.md) - directrices de codificación.
* [Refactorización de SocialUtils](/help/communities/socialutils.md) : asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales.

## Editor principal {#primary-publisher}

Cuando la implementación es un conjunto de servidores de publicación, es necesario identificar un editor principal que sondeará los artículos programados para publicarse.

Consulte [Editor principal](/help/communities/deploy-communities.md#primary-publisher) para obtener más información.

## Permitir medios enriquecidos {#allowing-rich-media}

La plataforma AEM bloquea los vínculos de otros sitios web para evitar los ataques XSS tal como se describe en

* [Protect contra scripts en sitios múltiples (XSS)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

A partir de AEM 6.2, las modificaciones que anteriormente se requerían realizar manualmente se incluyen en el archivo de configuración predeterminado AntiSamy.

El contenido multimedia enriquecido se incrusta en un artículo de blog seleccionando la variable `Embed Media from External Sites` icono :

![media](assets/media-icon.png)
