---
title: AEM Forms en grupos y privilegios OSGi
seo-title: AEM Forms en grupos y privilegios OSGi
description: Asignación de usuarios a los grupos para administrar los formularios AEM en OSGi
seo-description: Asignación de usuarios a los grupos para administrar los formularios AEM en OSGi
uuid: f269a206-356d-4cee-b449-05c5da87121a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
topic-tags: Configuration
discoiquuid: 1717b1b4-1c2a-450e-8e79-4156a974d5fa
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247

---


# AEM Forms en grupos y privilegios OSGi{#aem-forms-on-osgi-groups-and-privileges}

Puede [crear grupos](/help/sites-administering/user-group-ac-admin.md#group-administration) y asignar políticas y [usuarios](/help/sites-administering/user-group-ac-admin.md#user-administration) a los grupos en AEM. Estas directivas controlan los privilegios de los usuarios que forman parte del grupo.

Una vez que instale el paquete [de complementos de formularios](../../forms/using/installing-configuring-aem-forms-osgi.md)AEM, los grupos mencionados en este artículo, como el usuario de formularios y el usuario que puede utilizar formularios, estarán disponibles automáticamente para su asignación. En la tabla siguiente se enumeran las tareas que un usuario puede realizar para AEM Forms en OSGi según las asignaciones de grupo:

<table>
 <tbody>
  <tr>
   <td>Agrupar</td> 
   <td>Tareas</td> 
  </tr>
  <tr>
   <td>form-user <sup><a href="#main-pars-text">[1]</a></sup></td> 
   <td>
    <ul> 
     <li>Creación, vista previa, publicación y envío de formularios adaptables</li> 
     <li>Creación, vista previa y publicación de comunicaciones interactivas y fragmentos de documentos</li> 
     <li>Carga de recursos en una instancia de AEM</li> 
     <li>Creación de temas</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>forms-power-user</td> 
   <td>
    <ul> 
     <li>Creación, vista previa, publicación y envío de formularios adaptables</li> 
     <li>Creación, vista previa y publicación de comunicaciones interactivas y fragmentos de documentos</li> 
     <li>Creación de secuencias de comandos para formularios adaptables mediante el editor de código</li> 
     <li>Carga de recursos, incluidas secuencias de comandos</li> 
     <li>Creación de temas</li> 
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
   <td>templates-author <sup><a href="#main-pars-text">[2]</a></sup></td> 
   <td>
    <ul> 
     <li>Creación y vista previa de formularios adaptables o plantillas de comunicaciones interactivas</li> 
    </ul> </td> 
  </tr>
  <tr>
   <td>template-power-user</td> 
   <td>
    <ul> 
     <li>Creación y vista previa de formularios adaptables o plantillas de comunicaciones interactivas</li> 
     <li>Creación de secuencias de comandos para formularios adaptables o plantillas de comunicaciones interactivas mediante el editor de código</li> 
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
     <li>Usar aplicaciones<br /> de bandeja de entrada de AEM <strong>Nota: Para acceder a la interfaz de usuario de Interactive Communications Agent en la bandeja de entrada de AEM, </strong>debe tener asignaciones de grupo de cm-agent-users y de usuarios de flujo de trabajo.</li> 
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

