---
title: Aspectos básicos de la garantía de calidad
seo-title: Aspectos básicos de la garantía de calidad
description: Función de foro de preguntas y respuestas
seo-description: Función de foro de preguntas y respuestas
uuid: c718a8e3-b3bd-4db9-8c0f-6dd973d40583
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: ceace3aa-78a5-485e-b519-630479e087d8
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# Aspectos básicos de la garantía de calidad {#qna-essentials}

Esta página proporciona la información esencial para trabajar con la función de foro de preguntas y respuestas (QnA).

## Esenciales para el cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>social/qna/components/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">inclusible</a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientllibs</a></td>
   <td>cq.ckeditor<br /> cq.social.hbs.vote<br /> cq.social.hbs.qna</td>
  </tr>
  <tr>
   <td> templates</td>
   <td> /libs/social/qna/components/hbs/qnaforum/qnaforum.hbs<br /> /libs/social/qna/components/hbs/qnaforum/activity-title.hbs</td>
  </tr>
  <tr>
   <td> css</td>
   <td> /libs/social/qna/components/hbs/qnaforum/clientlibs/qnaforum.css</td>
  </tr>
  <tr>
   <td> propiedades</td>
   <td>Consulte Función de foro <a href="working-with-qna.md">de preguntas y respuestas</a></td>
  </tr>
 </tbody>
</table>

* [Personalizaciones del lado del cliente](client-customize.md)

## Esenciales para servidor {#essentials-for-server-side}

* [API de QnA](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [Puntos finales de QnA](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

### Función Preguntas y respuestas {#qna-function}

Una estructura de sitio de comunidad que incluya la función [](functions.md#qna-function) QnA tendrá un componente `QnA` configurado, así como una configuración que afecta a la moderación y el etiquetado. La función QnA admite la identificación de un grupo [de usuarios miembros con](users.md#privileged-members-group)privilegios.

### Acceso a las publicaciones del foro de control de calidad (UGC) {#accessing-qna-forum-posts-ugc}

La UGC debe moderarse utilizando uno de los métodos estándar de moderación.
Consulte [Moderación del contenido](moderate-ugc.md)generado por el usuario.

A partir de AEM 6.1 Communities, el uso de un almacén [](working-with-srp.md) común para UGC incluye acceso mediante programación a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte:

* [Información general](srp.md) del proveedor de recursos de almacenamiento de información: introducción y uso del repositorio
* [Elementos esenciales](srp-and-ugc.md) de SRP y UGC: métodos y ejemplos de utilidad SRP
* [Acceso a UGC con SRP](accessing-ugc-with-srp.md) : directrices de codificación
* [Refactorización](socialutils.md) de SocialUtils: asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales

