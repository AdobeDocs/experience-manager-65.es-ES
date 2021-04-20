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
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 2%

---


# AEM Forms en grupos y privilegios OSGi{#aem-forms-on-osgi-groups-and-privileges}

Puede [crear grupos](/help/sites-administering/user-group-ac-admin.md#group-administration) y asignar directivas y [usuarios](/help/sites-administering/user-group-ac-admin.md#user-administration) a los grupos de AEM. Estas políticas controlan los privilegios de los usuarios que forman parte del grupo.

Una vez que instale [AEM Forms add-on package](../../forms/using/installing-configuring-aem-forms-osgi.md), los grupos mencionados en este artículo, como los usuarios de formularios y los usuarios con capacidad para formularios, estarán disponibles automáticamente para su asignación. La siguiente tabla enumera las tareas que un usuario puede realizar para AEM Forms en OSGi en función de las asignaciones de grupo:

<table>
 <tbody>
  <tr>
   <td>Agrupar</td> 
   <td>Tareas</td> 
  </tr>
  <tr>
   <td>usuarios de formularios <sup>[1]</sup></td> 
   <td>
    <ul> 
     <li>Crear, previsualizar, publicar y enviar formularios adaptables</li> 
     <li>Crear, previsualizar y publicar comunicaciones interactivas y fragmentos de documento</li> 
     <li>Cargar recursos a una instancia de AEM</li> 
     <li>Crear temas</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-users</td> 
   <td>
    <ul> 
     <li>Crear, previsualizar, publicar y enviar formularios adaptables</li> 
     <li>Crear, previsualizar y publicar comunicaciones interactivas y fragmentos de documento</li> 
     <li>Creación de secuencias de comandos para formularios adaptables mediante el editor de código</li> 
     <li>Carga de recursos, incluidas secuencias de comandos</li> 
     <li>Crear temas</li> 
     <li>Importar paquetes que contengan XDP</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-submit-reviewers</td> 
   <td>
    <ul> 
     <li>Revisar presentaciones</li> 
     <li>Aprobar o rechazar presentaciones</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>autores de plantillas <sup>[2]</sup></td> 
   <td>
    <ul> 
     <li>Creación y previsualización de formularios adaptables o plantillas de comunicaciones interactivas</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td><p>fdm-authors</p> </td> 
   <td>
    <ul> 
     <li>Creación y modificación de un modelo de datos de formulario</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>cm-agent-users</td> 
   <td>
    <ul> 
     <li>Acceda a cartas de gestión de correspondencia o comunicaciones interactivas mediante la interfaz de usuario del agente</li> 
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
   <td>flujo de trabajo-usuarios</td> 
   <td>
    <ul> 
     <li>Utilice AEM aplicaciones de bandeja de entrada<br /> <strong>Nota: </strong>Debe tener asignaciones de grupo cm-agent-users y workflow-users para acceder a la interfaz de usuario de Interactive Communications Agent en AEM bandeja de entrada.</li> 
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

