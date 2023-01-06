---
title: AEM Forms en grupos y privilegios de OSGi
seo-title: AEM Forms on OSGi Groups and Privileges
description: Asignar usuarios a los grupos para administrar AEM Forms en OSGi
seo-description: Assign users to the groups to manage AEM Forms on OSGi
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
role: Admin
exl-id: d802ac53-e3db-45ca-afcb-7e99d0bb7877
source-git-commit: 603518dbe3d842a08900ac40651919c55392b573
workflow-type: ht
source-wordcount: '261'
ht-degree: 100%

---

# AEM Forms en grupos y privilegios de OSGi{#aem-forms-on-osgi-groups-and-privileges}

Puede [crear grupos](/help/sites-administering/user-group-ac-admin.md#group-administration) y asignar políticas y [usuarios](/help/sites-administering/user-group-ac-admin.md#user-administration) a los grupos de AEM. Estas políticas controlan los permisos de los usuarios que forman parte del grupo.

Una vez realizada la instalación del [paquete de complementos de AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md), los grupos mencionados en este artículo, como forms-users y forms-power-user, estarán disponibles automáticamente para su asignación. La siguiente tabla muestra una lista de las tareas que un usuario puede realizar para AEM Forms en OSGi en función de las asignaciones de grupo:

<table>
 <tbody>
  <tr>
   <td>Grupo</td> 
   <td>Tareas</td> 
  </tr>
  <tr>
   <td>forms-users <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>Crear, previsualizar, publicar y enviar formularios adaptables</li> 
     <li>Crear, previsualizar y publicar comunicaciones interactivas y fragmentos de documentos</li> 
     <li>Cargar recursos en una instancia de AEM</li> 
     <li>Crear temáticas</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-users</td> 
   <td>
    <ul> 
     <li>Crear, previsualizar, publicar y enviar formularios adaptables</li> 
     <li>Crear, previsualizar y publicar comunicaciones interactivas y fragmentos de documentos</li> 
     <li>Crear scripts para formularios adaptables mediante el editor de código</li> 
     <li>Cargar recursos, incluidos scripts</li> 
     <li>Crear temáticas</li> 
     <li>Importar paquetes que contengan XDP</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-submission-reviewers</td> 
   <td>
    <ul> 
     <li>Revisar envíos</li> 
     <li>Aprobar o rechazar envíos</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>template-authors <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>Crear y previsualizar formularios adaptables o plantillas de comunicaciones interactivas</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm-authors</p> </td> 
   <td>
    <ul> 
     <li>Crear y modificar un modelo de datos de formulario</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>Acceder a cartas de Administración de correspondencia o Interactive Communications mediante la interfaz de usuario del agente</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>workflow-editors</p> </td> 
   <td>
    <ul> 
     <li>Crear una aplicación de la bandeja de entrada</li> 
     <li>Crear un modelo del flujo de trabajo</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>workflow-users</td> 
   <td>
    <ul> 
     <li>Usar aplicaciones de la Bandeja de entrada de AEM<br /> <strong>Nota:</strong> Debe tener asignaciones de los grupos cm-agent-users y workflow-users para acceder a la interfaz de usuario del agente de Interactive Communications en la Bandeja de entrada de AEM.</li> 
     <li>Administrar instancias de flujo de trabajo</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>fd-administrators</td> 
   <td>
    <ul> 
     <li>Configurar PDF Generator</li> 
     <li>Configurar carpetas inspeccionadas</li> 
     <li>Administrar aplicaciones de flujo de trabajo</li> 
    </ul> </td> 
  </tr>
 </tbody>
</table>

1. El usuario con privilegios del grupo forms-users no puede escribir scripts para formularios adaptables.
1. El usuario con privilegios del grupo de autores de plantillas no puede escribir scripts para plantillas.
