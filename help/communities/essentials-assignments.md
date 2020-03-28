---
title: Ascripciones esenciales
seo-title: Ascripciones esenciales
description: Descripción general de la función Asignaciones para comunidades de habilitación
seo-description: Descripción general de la función Asignaciones para comunidades de habilitación
uuid: e49fce26-1091-4f37-93e8-c4ec85371811
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 6bac681e-59e1-4786-9c50-6679c936cfd1
docset: aem65
translation-type: tm+mt
source-git-commit: 0b25d956c19c5fc5d79f87b292a0c61a23e5d66a

---


# Ascripciones esenciales {#assignments-essentials}

Siga leyendo para conocer la información esencial para trabajar con la función de asignaciones de los sitios de comunidad [de](/help/communities/overview.md#enablement-community) habilitación.

La función de asignaciones es la capacidad de asignar recursos de habilitación y rutas de aprendizaje a miembros de comunidades de habilitación.

## Esenciales para el cliente {#essentials-for-client-side}

<table>
 <tbody>
  <tr>
   <td> <strong>resourceType</strong></td>
   <td>social/habilitación/componentes/hbs/miasignados</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/scf.md#add-or-include-a-communities-component"><strong>inclusible</strong></a></td>
   <td>No</td>
  </tr>
  <tr>
   <td> <a href="/help/communities/clientlibs.md"><strong>clientllibs</strong></a></td>
   <td>cq.social.enablement.hbs.breadcrumbs<br /> cq.social.enablement.hbs.mysigned<br /> cq.social.enablement.hbs.resource<br /> cq.social.enablement.hbs.learningPath</td>
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
   <td>Consulte Función <a href="/help/communities/assignments.md">Asignaciones</a></td>
  </tr>
 </tbody>
</table>

### Estado de finalización y éxito {#completion-and-success-status}

El estado de Finalización y Éxito se utiliza en los informes y las pancartas de estado de las asignaciones.

Estado de finalización:

* Sin asignar
* No iniciado (nuevo)
* En curso
* Completar

Estado de éxito:

* Desconocido
* Pase
* Error

Las únicas combinaciones posibles de estado de finalización y éxito son:

| **Finalización** | **Correcto** |
|---|---|
| Sin iniciar | Desconocido |
| En curso | Desconocido |
| Completar | Pase |
| Completar | Error |

## Esenciales para servidor {#essentials-for-server-side}

### Función Asignaciones {#assignments-function}

Una estructura de sitio de comunidad que incluye la función [](/help/communities/functions.md#assignments-function)Asignaciones incluye un ` [assignments](/help/communities/assignments.md)` componente configurado.

### API de referencia {#reference-apis}

* [API de habilitación](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/enablement/reporting/model/api/package-summary.html)

* [API de Sistema de informes](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/dv/api/package-summary.html)

* [API de Sistema de informes Analytics](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/cq/social/reporting/analytics/api/package-summary.html)

