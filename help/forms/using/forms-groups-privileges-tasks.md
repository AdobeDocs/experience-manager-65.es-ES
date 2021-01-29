---
title: AEM Forms en grupos y privilegios OSGi
seo-title: AEM Forms en grupos y privilegios OSGi
description: Asignar usuarios a los grupos para administrar AEM Forms en OSGi
seo-description: Asignar usuarios a los grupos para administrar AEM Forms en OSGi
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
translation-type: tm+mt
source-git-commit: a4314a30e2329aebe02f4983fd543240be920ee8
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 1%

---


# AEM Forms en grupos OSGi y privilegios{#aem-forms-on-osgi-groups-and-privileges}

Puede [crear grupos](/help/sites-administering/user-group-ac-admin.md#group-administration) y asignar directivas y [usuarios](/help/sites-administering/user-group-ac-admin.md#user-administration) a los grupos de AEM. Estas directivas controlan los privilegios de los usuarios que forman parte del grupo.

Una vez que instale [paquete de complementos de AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md), los grupos mencionados en este artículo, como usuarios de formularios y usuarios avanzados, estarán disponibles automáticamente para su asignación. La siguiente tabla lista las tareas que un usuario puede realizar para AEM Forms en OSGi en función de las asignaciones de grupo:

<table>
 <tbody>
  <tr>
   <td>Agrupar</td> 
   <td>Tareas</td> 
  </tr>
  <tr>
   <td>forms-users <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>Creación, previsualización, publicación y envío de formularios adaptables</li> 
     <li>Creación, previsualización y publicación de comunicaciones interactivas y fragmentos de documento</li> 
     <li>Carga de recursos en una instancia de AEM</li> 
     <li>Crear temáticas</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-users</td> 
   <td>
    <ul> 
     <li>Creación, previsualización, publicación y envío de formularios adaptables</li> 
     <li>Creación, previsualización y publicación de comunicaciones interactivas y fragmentos de documento</li> 
     <li>Creación de secuencias de comandos para formularios adaptables mediante el editor de código</li> 
     <li>Carga de recursos, incluidas secuencias de comandos</li> 
     <li>Crear temáticas</li> 
     <li>Importar paquetes que contengan XDP</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-submit-reviewers</td> 
   <td>
    <ul> 
     <li>Revisar envíos</li> 
     <li>Aprobar o rechazar envíos</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>templates-author <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>Creación y previsualización de formularios adaptables o plantillas de comunicaciones interactivas</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm-author</p> </td> 
   <td>
    <ul> 
     <li>Crear y modificar un modelo de datos de formulario</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>Acceso a cartas de Correspondencia o comunicaciones interactivas mediante la interfaz de usuario del agente</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> 
     <li>Creación de una aplicación de bandeja de entrada</li> 
     <li>Creación de un modelo de flujo de trabajo</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>flujos de trabajo-usuarios</td> 
   <td>
    <ul> 
     <li>Utilice AEM aplicaciones de bandeja de entrada<br /> <strong>Nota: </strong>Debe tener asignaciones de cm-agent-users y grupos de usuarios de flujo de trabajo para acceder a la interfaz de usuario de Interactive Communications Agent en AEM bandeja de entrada.</li> 
     <li>Administrar instancias de flujo de trabajo</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>fd-administradores</td> 
   <td>
    <ul> 
     <li>Configurar generador de PDF</li> 
     <li>Configurar carpeta vigilada</li> 
     <li>Administrar aplicaciones de flujo de trabajo</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. El usuario con privilegios de grupo de usuarios de formularios no puede escribir secuencias de comandos para formularios adaptables.
1. El usuario con privilegios de grupo de autores de plantillas no puede escribir secuencias de comandos para plantillas.

