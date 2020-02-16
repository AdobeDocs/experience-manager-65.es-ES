---
title: Elementos esenciales del blog
seo-title: Elementos esenciales del blog
description: Información general del blog
seo-description: Información general del blog
uuid: 714cf70c-76a0-4be6-9163-a31ac6bd1643
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: eece7b8f-6ccd-4037-8713-0cd36cfd9e73
docset: aem65
translation-type: tm+mt
source-git-commit: 44eb94b917fe88b7c90c29ec7da553e15be391db

---


# Elementos esenciales del blog{#blog-essentials}

Desde AEM 6.1 Communities, un blog es una actividad comunitaria. Los artículos de blog ahora se publican desde el entorno de publicación, donde anteriormente los artículos de blog solo podían crearse en el entorno de creación y publicarse.

Los artículos de blog ahora pueden ser creados por cualquier miembro de la comunidad, a menos que estén restringidos a miembros privilegiados.

Esta página proporciona la información esencial para trabajar con la función de blog.

>[!NOTE]
>
>La infraestructura subyacente de la función de blog es la función de diario.

## Esenciales para el cliente {#essentials-for-client-side}

La función de blog consta de dos componentes principales disponibles mediante la adición de la función [](/help/communities/functions.md#blog-function) Blog o la adición de los componentes a una página en modo de edición de autor.

### Blog {#blog}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/diario/componentes/hbs/diario</td>
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
   <td>consulte Función <a href="/help/communities/blog-feature.md">de blog</a></td>
  </tr>
 </tbody>
</table>

### Barra lateral de blog {#blog-sidebar}

| **resourceType** | social/diario/componentes/hbs/barra lateral |
|---|---|
| [**inclusible **](/help/communities/scf.md#add-or-include-a-communities-component) | No |
| [**clientllibs **](/help/communities/clientlibs.md) | cq.social.hbs.journal_sidebar |
| **templates** | /libs/social/journal/components/hbs/sidebar/sidebar.hbs |
| **css** | /libs/social/journal/components/hbs/sidebar/clientlibs/sidebar.css |
| **propiedades** | consulte Función [de blog](/help/communities/blog-feature.md) |

* [Personalizaciones del lado del cliente](/help/communities/client-customize.md)

## Esenciales para servidor {#essentials-for-server-side}

* [API de blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/api/package-summary.html)

* [Extremos de blog](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/journal/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](/help/communities/server-customize.md)

### Función Blog {#blog-function}

Una estructura de sitio de comunidad que incluye la función [](/help/communities/functions.md#blog-function) Blog tendrá componentes `Blog` y `Blog Sidebar` configurados. La función Blog permite identificar un grupo [de usuarios miembros](/help/communities/users.md#privileged-members-group)privilegiados.

### Acceso a entradas de blog (UGC) {#accessing-blog-entries-ugc}

La UGC debe moderarse utilizando uno de los métodos estándar de moderación.
Consulte [Moderación del contenido](/help/communities/moderate-ugc.md)generado por el usuario.

A partir de AEM 6.1 Communities, el uso de un almacén [](/help/communities/working-with-srp.md) común para UGC incluye acceso mediante programación a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte :

* [Información general](/help/communities/srp.md) del proveedor de recursos de almacenamiento de información: introducción y uso del repositorio
* [Elementos esenciales](/help/communities/srp-and-ugc.md) de SRP y UGC: métodos y ejemplos de utilidad SRP
* [Acceso a UGC con SRP](/help/communities/accessing-ugc-with-srp.md) : directrices de codificación
* [Refactorización](/help/communities/socialutils.md) de SocialUtils: asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales

## Editor principal {#primary-publisher}

Cuando la implementación es un conjunto de servidores de publicación, es necesario identificar un editor principal que sondeará los artículos programados para publicarse.

Consulte Editor [principal](/help/communities/deploy-communities.md#primary-publisher) para obtener más información.

## Permitir medios enriquecidos {#allowing-rich-media}

La plataforma AEM bloquea los vínculos de otros sitios web para evitar ataques XSS, tal como se describe en

* [Proteger contra secuencias de comandos entre sitios (XSS)](/help/sites-developing/security.md#protect-against-cross-site-scripting-xss)

A partir de AEM 6.2, las modificaciones que anteriormente se requerían manualmente se incluyen en el archivo de configuración predeterminado AntiSamy.

Los medios enriquecidos están incorporados en un artículo de blog seleccionando el `Embed Media from External Sites` icono :

![chlimage_1-199](assets/chlimage_1-199.png)

