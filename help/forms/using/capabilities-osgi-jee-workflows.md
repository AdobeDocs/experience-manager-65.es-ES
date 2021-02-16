---
title: Acciones y capacidades de los Flujos de trabajo de AEM centrados en formularios en los flujos de trabajo OSGi y AEM Forms JEE
description: Acciones y capacidades de los Flujos de trabajo de AEM centrados en formularios en los flujos de trabajo OSGi y AEM Forms JEE
contentOwner: khsingh
translation-type: tm+mt
source-git-commit: dfa5a0dbfdd2c63ea0ec66d805e8b452baa3d0ac
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 22%

---


# Acciones y capacidades de los Flujos de trabajo de AEM centrados en el formulario en los flujos de trabajo OSGi y AEM Forms JEE {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## Bandeja de entrada AEM y espacio de trabajo HTML {#aem-inbox-and-html-workspace}

Puede utilizar AEM Bandeja de entrada para ejecutar y supervisar Flujos de trabajo de AEM centrados en Forms en OSGi. Mientras que HTML Workspace le permite ejecutar y supervisar Flujos de trabajo AEM Forms JEE. La siguiente tabla le ayuda a comprender varias acciones importantes disponibles en AEM Bandeja de entrada para Flujos de trabajo de AEM centrados en Forms en OSGi y en el espacio de trabajo HTML para Flujos de trabajo JEE de AEM Forms.

<table>
 <tbody>
  <tr>
   <td>Acciones</td>
   <td>Bandeja de entrada AEM</td>
   <td>Espacio de trabajo HTML</td>
  </tr>
  <tr>
   <td>Inicio de un proceso, tarea o aplicación de formulario<br /> </td>
   <td>Compatible<br /> </td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Envío de tareas</td>
   <td>Compatible<br /> </td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Asignación de una tarea a un grupo</td>
   <td>Compatible<br /> </td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Envío a varias rutas</td>
   <td>Compatible<br /> </td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Historial de tareas de seguimiento y resumen de tareas</td>
   <td>Compatible<br /> </td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Notificaciones por correo electrónico</td>
   <td>Compatible<br /> </td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Reasignación de tareas</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Datos adjuntos a nivel de campo para formularios adaptables</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Vista del calendario</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Comentarios de nivel de tarea</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Colas (cola personal compartida, reclamar tareas de la cola)</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Notificación fuera de la oficina</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
    <tr>
   <td>Personalización de elementos de la interfaz de usuario</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Asignación de una tarea a varios usuarios</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
 </tbody>
</table>

## Flujos de trabajo de AEM centrados en el formulario en Flujos de trabajo OSGi y AEM Forms JEE {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

Los Flujos de trabajo de AEM centrados en el formulario en OSGi y Flujos de trabajo AEM Forms JEE (AEM Forms en la administración de procesos JEE) tienen un conjunto diferente de funciones. La siguiente tabla le ayuda a comprender las funciones importantes disponibles en los Flujos de trabajo de AEM centrados en el formulario en OSGi y AEM Forms en Flujos de trabajo JEE:

<table>
 <tbody>
  <tr>
   <td>Capacidades</td>
   <td>Flujos de trabajo de AEM centrados en el formulario en OSGi<br /> </td>
   <td>flujos de trabajo JEE de AEM Forms</td>
  </tr>
  <tr>
   <td>Formularios adaptables</td>
   <td>Compatible</td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Integración con otras soluciones AEM</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Firma a mano alzada</td>
   <td>Compatible</td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Plantillas de correo electrónico personalizadas</td>
   <td>Compatible</td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Definición de la prioridad de tarea</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Tiempo de espera de una tarea después de la fecha de vencimiento</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Bucles dentro del flujo de trabajo</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Selección dinámica de un usuario asignado </td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Uso de metadatos personalizados</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Firma electrónica (Adobe Sign)</td>
   <td>Compatible con <sup>[1]</sup></td>
   <td>Compatible con <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>Administración de tareas y aplicaciones de formularios</td>
   <td>Compatible con <sup>[2]</sup><br /> </td>
   <td>Compatible con <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>Servicios de documento</td>
   <td>Compatible con <sup>[3]</sup></td>
   <td>Compatible con <sup>[3]</sup></td>
  </tr>
  <tr>
   <td>Representar la tarea completada como formulario adaptable o documento PDF</td>
   <td>Compatible</td>
   <td>Compatible [4]</td>
  </tr>
  <tr>
   <td>Integración con la administración de correspondencia</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
   <tr>
   <td>Gateways, SIN ESPERANZA </td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
   <tr>
   <td>Variables para almacenar datos </td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>O, Y Dividir</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>avatar de usuario</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Enviar un correo electrónico al final del flujo de trabajo</td>
   <td>Compatible con <sup>[7]</sup></td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Llamar a un servicio Web desde un flujo de trabajo</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Firma digital</td>
   <td>Compatible<br /> </td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Botón Restablecer</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Fases de flujo de trabajo</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Formularios adaptables de solo lectura</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Ocultar el botón de guardado predeterminado</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Control granular sobre la sección de detalles del flujo de trabajo</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Servicio de encuestas y programación</td>
   <td>Disponible de inmediato</td>
   <td>Se requiere implementación personalizada</td>
  </tr>
  <tr>
   <td>Aplicación adaptable de Forms</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Servicio del ensamblador</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Servicio Generator de PDF</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Servicio de Forms</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Servicio de salida</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Documento Assurance</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Ejecutar script</td>
   <td>Admite ECMAScript</td>
   <td>Admite fragmentos de código Java</td>
  </tr>
  <tr>
   <td>Ensamblador</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>  
  <tr>
   <td>HTML5 Forms, PDF forms interactivos, conjunto de formularios</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Informes de procesos</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Firma digital</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Categorías de punto de partida</td>
   <td>No compatible </td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Aprobación de tarea masiva </td>
   <td>No compatible </td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Guardar borrador con un nombre personalizado</td>
   <td>No compatible </td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Iniciar un proceso con datos de proceso existentes<br /> </td>
   <td>No compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Guardar un punto de partida como borrador</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Vista del administrador</td>
   <td>No compatible</td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Plantillas de búsqueda</td>
   <td>No compatible</td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Integración con aplicaciones de terceros</td>
   <td>No admitido <sup>[6]</sup></td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Datos adjuntos de nivel de tarea para aplicaciones de flujo de trabajo o puntos de inicio</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Correo electrónico del recordatorio</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Cambiar título en tiempo de espera de tarea</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Correo electrónico sobre delegación de tarea y solicitud de tarea</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Delegar entre grupos desunidos</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Transformación XSLT</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Prioridad de tarea dinámica</td>
   <td>No compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Título dinámico</td>
   <td>No compatible</td>
   <td>No compatible</td>
  </tr>
    <tr>
   <td>Descripción dinámica</td>
   <td>No compatible</td>
   <td>No compatible</td>
  </tr>
 </tbody>
</table>

1. Puede utilizar Flujos de trabajo de AEM centrados en el formulario en OSGi para firmar un formulario adaptable rellenado. Los Flujos de trabajo de AEM centrados en el formulario en OSGi son compatibles con la firma fuera del formulario. No se admite la experiencia de [firma en el formulario](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience).

1. Se requiere acceso a AEM Bandeja de entrada para ejecutar y supervisar flujos de trabajo centrados en el formulario en AEM Forms OSGi y HTML Workspace para ejecutar y supervisar Flujos de trabajo AEM Forms JEE.
1. Los servicios nativos de Documento de AEM Forms están disponibles para Flujos de trabajo de AEM centrados en el formulario en OSGi y AEM Forms en Flujos de trabajo JEE. AEM flujo de trabajo utiliza servicios de documento nativos para Flujos de trabajo de AEM centrados en formularios en Flujos de trabajo OSGi y AEM Forms JEE (Process Management).
1. Los Flujos de trabajo JEE de AEM Forms solo pueden procesar un formulario adaptable. No admite el procesamiento de un formulario adaptable como documento PDF.
1. Los Flujos de trabajo JEE de AEM formularios no tienen un paso independiente para Adobe Sign. Se requiere un formulario adaptable habilitado para Adobe Sign para AEM formularios Flujos de trabajo JEE. Para obtener más información, consulte la [documentación de Adobe Sign](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. Puede utilizar el paso [Invocar el servicio del modelo de datos de formulario](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) para invocar un servicio Web y publicar o recuperar datos de una aplicación de terceros.
1. Puede utilizar el paso [Enviar correo electrónico](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) para enviar correos electrónicos.

## Diferencias entre las funciones de la bandeja de entrada de AEM y la aplicación de AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Dos de las formas destacadas de iniciar un flujo de trabajo centrado en Forms son utilizar la [Bandeja de entrada de AEM](../../forms/using/manage-applications-inbox.md) y la aplicación de AEM Forms. Sin embargo, las capacidades de AEM bandeja de entrada y aplicación de AEM Forms difieren. AEM bandeja de entrada solo funciona con [flujos de trabajo centrados en Forms](../../forms/using/aem-forms-workflow.md) mientras que la aplicación de AEM Forms funciona tanto con flujos de trabajo centrados en Forms como con administración de procesos.

La siguiente tabla lista las funciones de AEM bandeja de entrada y aplicación de AEM Forms:

<table>
 <tbody>
  <tr>
   <td><p><strong>Acciones</strong></p> </td>
   <td><p><strong>Bandeja de entrada AEM</strong></p> </td>
   <td><p><strong>Aplicación de AEM Forms</strong></p> </td>
  </tr>
  <tr>
   <td><p>Inicio de una aplicación de formulario</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
  <tr>
   <td><p>Envío de tareas</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
  <tr>
   <td><p>Delegación de tareas</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>No compatible</p> </td>
  </tr>
  <tr>
   <td><p>Historial de tareas de seguimiento y resumen de tareas</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>No compatible</p> </td>
  </tr>
  <tr>
   <td><p>Añadir datos adjuntos de nivel de tarea</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
  <tr>
   <td><p>Visualización de datos adjuntos de nivel de tarea</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
  <tr>
   <td><p>Añadir datos adjuntos de nivel de campo</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
  <tr>
   <td><p>Visualización de la vista del calendario</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>No compatible</p> </td>
  </tr>
  <tr>
   <td><p>Adición de comentarios</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
 </tbody>
</table>

