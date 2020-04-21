---
title: Acciones y funciones de los Flujos de trabajo de AEM centrados en formularios en los flujos de trabajo OSGi y AEM Forms JEE
seo-title: Acciones y funciones de los Flujos de trabajo de AEM centrados en formularios en los flujos de trabajo OSGi y AEM Forms JEE
description: nulo
seo-description: nulo
uuid: 8af9527d-fa5e-4fcb-88e1-49571528fca6
contentOwner: khsingh
topic-tags: publish
discoiquuid: 89bcc76d-122f-4a3f-b857-16e5376e1624
docset: aem65
translation-type: tm+mt
source-git-commit: 0a2d53aa3eab4eb4ec58fa9b28bef675715b1d09

---


# Acciones y funciones de los Flujos de trabajo de AEM centrados en formularios en los flujos de trabajo OSGi y AEM Forms JEE {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## Bandeja de entrada de AEM y espacio de trabajo HTML {#aem-inbox-and-html-workspace}

Puede utilizar la Bandeja de entrada de AEM para ejecutar y supervisar Flujos de trabajo de AEM centrados en formularios en OSGi. Mientras que HTML Workspace le permite ejecutar y supervisar Flujos de trabajo JEE de AEM Forms. La siguiente tabla le ayuda a comprender las distintas acciones importantes disponibles en la Bandeja de entrada de AEM para Flujos de trabajo de AEM centrados en formularios en OSGi y en el espacio de trabajo HTML para Flujos de trabajo JEE de AEM Forms.

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
   <td>vista del calendario</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Comentarios de nivel de Tarea</td>
   <td>Compatible</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Colas (cola personal compartida, reclamar tareas de la cola)</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Notificación fuera de la oficina</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Asignación de una tarea a varios usuarios</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
 </tbody>
</table>

## Flujos de trabajo de AEM centrados en formularios en Flujos de trabajo OSGi y JEE de AEM Forms {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

Los Flujos de trabajo de AEM centrados en formularios en OSGi y Flujos de trabajo JEE de AEM Forms (AEM Forms en administración de procesos JEE) tienen un conjunto diferente de funciones. La siguiente tabla le ayuda a comprender las importantes funciones disponibles en los Flujos de trabajo de AEM centrados en el formulario en OSGi y AEM Forms en Flujos de trabajo JEE:

<table>
 <tbody>
  <tr>
   <td>Funciones</td>
   <td>Flujos de trabajo de AEM centrados en formularios en OSGi<br /> </td>
   <td>Flujos de trabajo JEE de AEM Forms</td>
  </tr>
  <tr>
   <td>Formularios adaptables</td>
   <td>Compatible</td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Integración con otras soluciones de AEM</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Firma de garabatos (obsoleta)</td>
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
   <td>Supported <sup>[1]</sup></td>
   <td>Supported <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>Administración de tareas y aplicaciones de formularios</td>
   <td>Supported <sup>[2]</sup><br /> </td>
   <td>Supported <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>Servicios de documentos</td>
   <td>Supported <sup>[3]</sup></td>
   <td>Supported <sup>[3]</sup></td>
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
   <td>Formularios HTML5, formularios PDF interactivos, conjunto de formularios<br /> </td>
   <td>No compatible<br /> </td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Informes de procesos</td>
   <td>No compatible<br /> </td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Firma digital</td>
   <td>Compatible<br /> </td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>categorías de punto de partida</td>
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
   <td>Iniciar un proceso con los datos de proceso existentes<br /> </td>
   <td>No compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Guardar un punto de partida como borrador</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>avatar de usuario</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>vista del administrador</td>
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
   <td>Not Supported <sup>[6]</sup></td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Datos adjuntos de nivel de Tarea para aplicaciones de flujo de trabajo o puntos de inicio</td>
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
   <td>Enviar un correo electrónico al final del flujo de trabajo</td>
   <td>Supported <sup>[7]</sup></td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Delegar entre grupos desunidos</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Llamar a un servicio Web desde un flujo de trabajo</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Transformación XSLT</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Gateways, SIN ESPERANZA </td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>O, Y Dividir</td>
   <td>No compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Prioridad de tarea dinámica</td>
   <td>No compatible</td>
   <td>No compatible</td>
  </tr>
 </tbody>
</table>

1. Puede utilizar Flujos de trabajo de AEM centrados en el formulario en OSGi para firmar un formulario adaptable rellenado. Los Flujos de trabajo de AEM centrados en el formulario en OSGi son compatibles con la firma fuera del formulario. No se admite la experiencia [de firma](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) en el formulario.

1. Es necesario acceder a la Bandeja de entrada de AEM para ejecutar y supervisar los flujos de trabajo centrados en el formulario en OSGi de AEM Forms y en HTML Workspace para ejecutar y supervisar los Flujos de trabajo JEE de AEM Forms.
1. Los servicios nativos de Documento de AEM Forms están disponibles para Flujos de trabajo de AEM centrados en el formulario en OSGi y AEM Forms en Flujos de trabajo JEE. AEM Workflow utiliza servicios de documento nativos para Flujos de trabajo de AEM centrados en formularios en Flujos de trabajo OSGi y AEM Forms JEE (Process Management).
1. Los Flujos de trabajo JEE de AEM Forms solo pueden procesar un formulario adaptable. No admite el procesamiento de un formulario adaptable como documento PDF.
1. Los Flujos de trabajo JEE de formularios AEM no tienen un paso independiente para Adobe Sign. Se requiere un formulario adaptable habilitado para Adobe Sign para Flujos de trabajo JEE de formularios AEM. Para obtener más información, consulte la documentación [de](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)Adobe Sign.
1. Puede utilizar el paso [Invocar el servicio](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) del modelo de datos de formulario para invocar un servicio Web y publicar o recuperar datos de una aplicación de terceros.
1. Puede utilizar el paso [Enviar correo electrónico](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) para enviar correos electrónicos.

## Diferencias entre las funciones de la bandeja de entrada de AEM y de la aplicación de AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Dos de las formas más importantes de iniciar un flujo de trabajo centrado en formularios son utilizar la bandeja de entrada [de](../../forms/using/manage-applications-inbox.md) AEM y la aplicación de AEM Forms. Sin embargo, las funciones de la bandeja de entrada de AEM y de la aplicación de AEM Forms difieren. La bandeja de entrada de AEM solo funciona con flujos de trabajo [centrados en](../../forms/using/aem-forms-workflow.md) formularios, mientras que la aplicación de AEM Forms funciona tanto con flujos de trabajo centrados en formularios como con la administración de procesos.

La tabla siguiente lista las funciones de la bandeja de entrada de AEM y la aplicación de AEM Forms:

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

