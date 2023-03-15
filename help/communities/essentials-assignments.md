---
title: Assignments Essentials
seo-title: Assignments Essentials
description: Información general sobre la función Asignaciones para comunidades de habilitación
seo-description: Assignments feature overview for enablement communities
uuid: e49fce26-1091-4f37-93e8-c4ec85371811
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 6bac681e-59e1-4786-9c50-6679c936cfd1
docset: aem65
exl-id: 75cef5da-4f93-4721-99c0-ad44c8ab76d4
source-git-commit: 1d334c42088342954feb34f6179dc5b134f81bb8
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 13%

---

# Assignments Essentials {#assignments-essentials}

Siga leyendo para conocer la información esencial para trabajar con la función de asignaciones de [comunidad de habilitación](/help/communities/overview.md#enablement-community) sitios.

La función de asignaciones permite asignar recursos de habilitación y rutas de aprendizaje a miembros de comunidades de habilitación.

## Essentials para el lado del cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/enablement/components/hbs/myassigned</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>incluible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientlibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadrumbs<br /> cq.social.enablement.hbs.myassigned<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningpath</td>
  </tr>
  <tr>
   <td> <strong>templates</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/myassigned.hbs</td>
  </tr>
  <tr>
   <td> <strong>css</strong></td>
   <td> /libs/social/enablement/components/hbs/myassigned/clientlibs/myassigned.css</td>
  </tr>
  <tr>
   <td><strong> propiedades</strong></td>
   <td>Consulte <a href="/help/communities/assignments.md">Función Asignaciones</a></td>
  </tr>
 </tbody>
</table>

### Estado de finalización y éxito {#completion-and-success-status}

Los estados de finalización y éxito se utilizan en los informes y en los titulares de estado de las Asignaciones.

Estado de finalización:

* Sin asignar
* Sin iniciar (nuevo)
* En curso
* Completar

Estado de éxito:

* Desconocido
* Pase
* Error

Las únicas combinaciones posibles de estado de éxito y finalización son las siguientes:

| **Finalización** | **Correcto** |
|---|---|
| Sin iniciar | Desconocido |
| En curso | Desconocido |
| Completar | Pase |
| Completar | Error |

## Essentials para servidor {#essentials-for-server-side}

### Función Asignaciones {#assignments-function}

Una estructura de sitio de la comunidad que incluye [Función Asignaciones](/help/communities/functions.md#assignments-function), incluye un configurado ` [assignments](/help/communities/assignments.md)` componente.

### API de referencia {#reference-apis}

* [API de habilitación](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [API de informes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [API de Reporting Analytics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/model/api/package-summary.html)
