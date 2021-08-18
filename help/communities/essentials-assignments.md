---
title: Ascripciones esenciales
seo-title: Ascripciones esenciales
description: Información general sobre la función Asignaciones para comunidades de habilitación
seo-description: Información general sobre la función Asignaciones para comunidades de habilitación
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
source-wordcount: '222'
ht-degree: 13%

---

# Ascripciones esenciales {#assignments-essentials}

Siga leyendo para conocer la información esencial para trabajar con la función de asignaciones de los sitios de [comunidad de habilitación](/help/communities/overview.md#enablement-community).

La función de asignaciones es la capacidad de asignar recursos de habilitación y rutas de aprendizaje a miembros de comunidades de habilitación.

## Elementos esenciales para el cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/habilitación/componentes/hbs/myassigned</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.myassigned<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learn.path</td>
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
   <td>Consulte <a href="/help/communities/assignments.md">Función de asignaciones</a></td>
  </tr>
 </tbody>
</table>

### Estado de finalización y éxito {#completion-and-success-status}

El estado de Finalización y Éxito se utiliza en los informes y los titulares de estado en Asignaciones.

Estado de finalización:

* Sin asignar
* No iniciado (nuevo)
* En curso
* Completar

Estado de éxito:

* Desconocido
* Pase
* Error

Las únicas combinaciones posibles de Estado de finalización y éxito son:

| **Finalización** | **Correcto** |
|---|---|
| Sin iniciar | Desconocido |
| En curso | Desconocido |
| Completar | Pase |
| Completar | Error |

## Elementos esenciales para el servidor {#essentials-for-server-side}

### Función Asignaciones {#assignments-function}

Una estructura de sitio de la comunidad que incluye la [Función de asignaciones](/help/communities/functions.md#assignments-function), incluye un componente ` [assignments](/help/communities/assignments.md)` configurado.

### API de referencia {#reference-apis}

* [API de habilitación](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [API de informes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [API de informes de Analytics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/model/api/package-summary.html)
