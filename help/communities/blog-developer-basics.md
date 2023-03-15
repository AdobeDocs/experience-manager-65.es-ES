---
title: Blog Essentials
seo-title: Blog Essentials
description: Resumen del blog
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

# Blog Essentials {#blog-essentials}

AEM A partir de las comunidades de 6.1 de, un blog es una actividad de la comunidad. Los artículos del blog ahora se publican desde el entorno de publicación, donde anteriormente, los artículos de blog solo se podían crear y publicar en el entorno de creación.

Los artículos de blog ahora pueden ser creados por cualquier miembro de la comunidad, a menos que estén restringidos a miembros privilegiados.

Esta página proporciona la información esencial para trabajar con la función de blog.

>[!NOTE]
>
>La infraestructura subyacente de la función de blog es la función de diario.

## Essentials para el lado del cliente {#essentials-for-client-side}

La función de blog consta de dos componentes principales que están disponibles al agregar el [Función Blog](/help/communities/functions.md#blog-function) o añadiendo los componentes a una página en modo de edición de autor.

### Blog {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/journal/components/hbs/journal</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>incluible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
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
   <td>consulte <a href="/help/communities/blog-feature.md">Función Blog</a></td>
  </tr>
 </tbody>
</table>

### Barra lateral de blog {#blog-sidebar}

| **resourceType** | social/journal/components/hbs/sidebar |
|---|---|
| [**incluible**](/help/communities/scf.md#add-or-include-a-communities-component) | No |
| [**clientlibs**](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **templates** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **propiedades** | consulte [Función Blog](/help/communities/blog-feature.md) |

* [Personalizaciones del lado del cliente](/help/communities/client-customize.md)

## Essentials para servidor {#essentials-for-server-side}

* [API de blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [Extremos del blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](/help/communities/server-customize.md)

### Función Blog {#blog-function}

Una estructura de sitio de la comunidad que incluye [Función Blog](/help/communities/functions.md#blog-function) habría configurado `Blog` y `Blog Sidebar` componentes. La función Blog admite la identificación de [grupo de usuarios miembros privilegiados](/help/communities/users.md#privileged-members-group).

### Acceso a las entradas de blog (UGC) {#accessing-blog-entries-ugc}

La UGC debe moderarse utilizando uno de los métodos habituales de moderación.
Consulte [Moderación del contenido generado por el usuario](/help/communities/moderate-ugc.md).

AEM A partir de la versión 6.1 de las comunidades de la, se utilizará [almacén común](/help/communities/working-with-srp.md) para UGC incluye acceso programático a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte :

* [Resumen del proveedor de recursos de almacenamiento](/help/communities/srp.md) - introducción y descripción general del uso del repositorio.
* [SRP y UGC Essentials](/help/communities/srp-and-ugc.md) - Métodos y ejemplos de la utilidad SRP.
* [Acceso a UGC con SRP](/help/communities/accessing-ugc-with-srp.md) - directrices de codificación.
* [Refactorización de SocialUtils](/help/communities/socialutils.md) : asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales.

## Editor principal {#primary-publisher}

Cuando la implementación es un conjunto de servidores de publicación, es necesario identificar un editor principal que sondeará los artículos programados para su publicación.

Consulte [Editor principal](/help/communities/deploy-communities.md#primary-publisher) para obtener más información.

## Permitir medios enriquecidos {#allowing-rich-media}

AEM La plataforma bloquea los vínculos de otros sitios web para evitar ataques XSS como se describe en

* [Protect con scripts en sitios múltiples (XSS)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

AEM A partir de la versión 6.2 de la versión, las modificaciones que se requerían anteriormente para realizarse manualmente se incluyen en el archivo de configuración predeterminado de AntiSamy.

Los medios enriquecidos se incrustan en un artículo de blog seleccionando la variable `Embed Media from External Sites` icono :

![media](assets/media-icon.png)
