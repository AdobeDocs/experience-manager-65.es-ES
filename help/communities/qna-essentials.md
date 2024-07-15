---
title: Aspectos básicos de QnA
description: Conozca los aspectos básicos del trabajo con la función de foro Preguntas y respuestas (QnA) en las comunidades de Adobe Experience Manager.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: a7b295c1-cc9d-4881-8016-804b21fc1098
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 2%

---

# Aspectos básicos de QnA {#qna-essentials}

Esta página proporciona la información esencial para trabajar con la función de foro preguntas y respuestas (QnA).

## Essentials para el lado del cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> resourceType</td>
   <td>social/qna/components/hbs/qnaforum</td>
  </tr>
  <tr>
   <td> <a href="scf.md#add-or-include-a-communities-component">incluir</a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="clientlibs.md">clientlibs</a></td>
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
   <td>Ver <a href="working-with-qna.md">función de foro de preguntas y respuestas</a></td>
  </tr>
 </tbody>
</table>

* [Personalizaciones del lado del cliente](client-customize.md)

## Essentials para servidor {#essentials-for-server-side}

* [API de QnA](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/qna/client/api/package-summary.html)

* [Puntos finales de QnA](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/cq/social/qna/client/endpoints/package-summary.html)

* [Personalizaciones del lado del servidor](server-customize.md)

### Función Preguntas y respuestas {#qna-function}

Una estructura de sitio de la comunidad que incluye la función [QnA](functions.md#qna-function) tiene un componente `QnA` configurado y opciones que afectan a la moderación y al etiquetado. La función QnA admite la identificación de un [grupo de usuarios miembros privilegiados](users.md#privileged-members-group).

### Acceso a las publicaciones del foro de control de calidad (UGC) {#accessing-qna-forum-posts-ugc}

La UGC debe moderarse utilizando uno de los métodos habituales de moderación.
Consulte [Moderar contenido generado por el usuario](moderate-ugc.md).

AEM A partir de las comunidades de la versión 6.1 de, el uso de un [almacén común](working-with-srp.md) para UGC incluye el acceso programático a UGC independientemente de la opción de almacenamiento elegida (como ASRP, MSRP o JSRP).

**La ubicación y el formato del UGC en el repositorio están sujetos a cambios sin previo aviso**.

Consulte:

* [Resumen del proveedor de recursos de almacenamiento](srp.md) - introducción y descripción general del uso del repositorio.
* [SRP y UGC Essentials](srp-and-ugc.md): métodos y ejemplos de utilidades SRP.
* [Acceder a UGC con SRP](accessing-ugc-with-srp.md): directrices de codificación.
* [Refactorización de SocialUtils](socialutils.md): asignación de métodos de utilidad obsoletos a métodos de utilidad SRP actuales.
