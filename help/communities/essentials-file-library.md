---
title: Esenciales de la biblioteca de archivos
seo-title: Esenciales de la biblioteca de archivos
description: Uso de la función de biblioteca de archivos
seo-description: Uso de la función de biblioteca de archivos
uuid: 0630f13e-97b4-4f93-9dce-07f559287c29
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 9019b967-fff8-4dda-bc5a-fd4a3e14a4ef
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Esenciales de la biblioteca de archivos {#file-library-essentials}

Esta página proporciona la información esencial para trabajar con la función de biblioteca de archivos.

## Esenciales para el cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/filelibrary/components/hbs/filelibrary</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.vote<br /> cq.social.hbs.filelibrary</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/filelibrary/components/hbs/filelibrary/filelibrary.hbs<br /> /libs/social/filelibrary/components/hbs/folder/folder.hbs<br /> /libs/social/filelibrary/components/hbs/folder/item.hbs<br /> /libs/social/filelibrary/components/hbs/document/document.hbs<br /> /libs/social/filelibrary/components/hbs/document/item.hbs<br /> </td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/filelibrary/components/hbs/filelibrary/clientlibs/filelibrary.css</td>
  </tr>
  <tr>
   <td><strong> propiedades</strong></td>
   <td>Consulte Función <a href="file-library.md">Biblioteca de archivos</a></td>
  </tr>
 </tbody>
</table>

* [Personalizaciones del lado del cliente](client-customize.md)

## Esenciales para servidor {#essentials-for-server-side}

* [API de la biblioteca de archivos](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/filelibrary/client/api/package-summary.html)

* [Extremos de la biblioteca de archivos](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/filelibrary/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

### Función Biblioteca del archivo {#file-library-function}

Una estructura de sitio de comunidad que incluye la función [Biblioteca de](functions.md#file-library-function)archivos incluye un `file library` componente configurado.

### Acceso a los comentarios publicados para bibliotecas de archivos (UGC) {#accessing-comments-posted-for-file-libraries-ugc}

La UGC debe moderarse utilizando uno de los métodos estándar de moderación.
Consulte [Moderación del contenido](moderate-ugc.md)generado por el usuario.

A partir de AEM 6.1 Communities, el uso de un almacén [](working-with-srp.md) común para UGC incluye acceso mediante programación a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte:

* [Información general](srp.md) del proveedor de recursos de almacenamiento de información: introducción y uso del repositorio
* [Elementos esenciales](srp-and-ugc.md) de SRP y UGC: métodos y ejemplos de utilidad SRP
* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) : directrices de codificación
* [Refactorización](socialutils.md) de SocialUtils: asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales

