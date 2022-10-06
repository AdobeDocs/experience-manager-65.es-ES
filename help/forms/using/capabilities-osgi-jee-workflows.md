---
title: Acciones y capacidades de los flujos de trabajo AEM centrados en formularios en los flujos de trabajo OSGi y AEM Forms JEE
description: Acciones y capacidades de los flujos de trabajo AEM centrados en formularios en los flujos de trabajo OSGi y AEM Forms JEE
contentOwner: khsingh
exl-id: 505b8988-b2b3-4222-b3cb-9b3c6259fdd2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 23%

---

# Acciones y capacidades de los flujos de trabajo AEM centrados en formularios en los flujos de trabajo OSGi y AEM Forms JEE {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## AEM bandeja de entrada y espacio de trabajo del HTML {#aem-inbox-and-html-workspace}

Puede utilizar AEM Bandeja de entrada para ejecutar y supervisar los flujos de trabajo de AEM centrados en Forms en OSGi. Por su parte, HTML Workspace le permite ejecutar y supervisar flujos de trabajo JEE de AEM Forms. La siguiente tabla le ayuda a comprender varias acciones importantes disponibles en AEM Bandeja de entrada para flujos de trabajo de AEM centrados en Forms en OSGi y en Espacio de trabajo de HTML para flujos de trabajo JEE de AEM Forms.

<table>
 <tbody>
  <tr>
   <td>Acciones</td>
   <td>Bandeja de entrada AEM</td>
   <td>HTML Workspace</td>
  </tr>
  <tr>
   <td>Inicio de un proceso, tarea o aplicación de formulario<br /> </td>
   <td>Compatibilidad<br /> </td>
   <td>Compatibilidad<br /> </td>
  </tr>
  <tr>
   <td>Envío de tareas</td>
   <td>Compatibilidad<br /> </td>
   <td>Compatibilidad<br /> </td>
  </tr>
  <tr>
   <td>Asignación de una tarea a un grupo</td>
   <td>Compatibilidad<br /> </td>
   <td>Compatibilidad<br /> </td>
  </tr>
  <tr>
   <td>Envío a varias rutas</td>
   <td>Compatibilidad<br /> </td>
   <td>Compatibilidad<br /> </td>
  </tr>
  <tr>
   <td>Historial de tareas de seguimiento y resumen de tareas</td>
   <td>Compatibilidad<br /> </td>
   <td>Compatibilidad<br /> </td>
  </tr>
  <tr>
   <td>Notificaciones por correo electrónico</td>
   <td>Compatibilidad<br /> </td>
   <td>Compatibilidad<br /> </td>
  </tr>
  <tr>
   <td>Reasignación de tareas</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Archivos adjuntos de nivel de campo para formularios adaptables</td>
   <td>Compatibilidad</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Vista de calendario</td>
   <td>Compatibilidad</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Comentarios de nivel de tarea</td>
   <td>Compatibilidad</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Colas (cola personal compartida, Reclamar tareas de la cola)</td>
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
   <td>Compatibilidad</td>
  </tr>
 </tbody>
</table>

## Flujos de trabajo de AEM centrados en formularios en flujos de trabajo de OSGi y AEM Forms JEE {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

Los flujos de trabajo de AEM centrados en formularios en OSGi y AEM Forms JEE Workflows (AEM Forms en JEE Process Management) tienen un conjunto diferente de funciones. La siguiente tabla le ayuda a comprender las importantes capacidades disponibles en Flujos de trabajo de AEM centrados en formularios en OSGi y AEM Forms en flujos de trabajo JEE:

<table>
 <tbody>
  <tr>
   <td>Capacidades</td>
   <td>Flujos de trabajo AEM centrados en formularios en OSGi<br /> </td>
   <td>Flujos de trabajo de AEM Forms JEE</td>
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
   <td>Firma manuscrita</td>
   <td>Compatible</td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Plantillas de correo electrónico personalizadas</td>
   <td>Compatible</td>
   <td>Compatible<br /> </td>
  </tr>
  <tr>
   <td>Definición de la prioridad de la tarea</td>
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
   <td>Admitido <sup>[1]</sup></td>
   <td>Admitido <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>Administrar aplicaciones de formularios y tareas</td>
   <td>Admitido <sup>[2]</sup><br /> </td>
   <td>Admitido <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>Servicios de documentos</td>
   <td>Admitido <sup>[3]</sup></td>
   <td>Admitido <sup>[3]</sup></td>
  </tr>
  <tr>
   <td>Representar una tarea completada como formulario adaptable o documento PDF</td>
   <td>Compatible</td>
   <td>Compatible [4]</td>
  </tr>
  <tr>
   <td>Integración con la gestión de correspondencia</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
   <tr>
   <td>Gateways , SIN ESPERA </td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
   <tr>
   <td>Variables para almacenar datos </td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>OR, Y División</td>
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
   <td>Admitido <sup>[7]</sup></td>
   <td>Compatibilidad</td>
  </tr>
  <tr>
   <td>Llamada a un servicio web desde un flujo de trabajo</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Firma digital</td>
   <td>Compatibilidad<br /> </td>
   <td>Compatibilidad<br /> </td>
  </tr>
  <tr>
   <td>Botón Restablecer</td>
   <td>Compatibilidad</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Etapas de flujo de trabajo</td>
   <td>Compatibilidad</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Formularios adaptables de solo lectura</td>
   <td>Compatibilidad</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Ocultar el botón de guardado predeterminado</td>
   <td>Compatibilidad</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Control granular sobre la sección de detalles del flujo de trabajo</td>
   <td>Compatibilidad</td>
   <td>No compatible</td>
  </tr>
  <tr>
   <td>Servicio de sondeo/programación</td>
   <td>Disponible de forma predeterminada</td>
   <td>Implementación personalizada requerida</td>
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
   <td>PDF Generator Service</td>
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
   <td>Document Assurance</td>
   <td>Compatible</td>
   <td>Compatible </td>
  </tr>
  <tr>
   <td>Ejecutar secuencia de comandos</td>
   <td>Admite ECMAScript</td>
   <td>Admite fragmentos de código Java</td>
  </tr>
  <tr>
   <td>Ensamblador</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>  
  <tr>
   <td>HTML 5 Forms, PDF forms interactivos, Conjunto de formularios</td>
   <td>No compatible</td>
   <td>Compatibilidad</td>
  </tr>
  <tr>
   <td>Informes de procesos</td>
   <td>No compatible</td>
   <td>Compatibilidad</td>
  </tr>
  <tr>
   <td>Firma digital</td>
   <td>Compatible</td>
   <td>Compatible</td>
  </tr>
  <tr>
   <td>Categorías de puntos de inicio</td>
   <td>No compatible </td>
   <td>Compatibilidad </td>
  </tr>
  <tr>
   <td>Aprobación de tareas masivas </td>
   <td>No compatible </td>
   <td>Compatibilidad </td>
  </tr>
  <tr>
   <td>Guardar borrador con un nombre personalizado</td>
   <td>No compatible </td>
   <td>Compatibilidad </td>
  </tr>
  <tr>
   <td>Inicio de un proceso con datos de proceso existentes<br /> </td>
   <td>No compatible</td>
   <td>Compatibilidad </td>
  </tr>
  <tr>
   <td>Guardar un punto de partida como borrador</td>
   <td>No compatible</td>
   <td>Compatibilidad</td>
  </tr>
  <tr>
   <td>Vista Administrador</td>
   <td>No compatible</td>
   <td>Compatibilidad<br /> </td>
  </tr>
  <tr>
   <td>Buscar conjunto de datos</td>
   <td>No compatible</td>
   <td>Compatibilidad<br /> </td>
  </tr>
  <tr>
   <td>Integración con aplicaciones de terceros</td>
   <td>No admitido <sup>[6]</sup></td>
   <td>Compatibilidad</td>
  </tr>
  <tr>
   <td>Archivos adjuntos de nivel de tarea para la aplicación de flujo de trabajo o el punto de inicio</td>
   <td>No compatible</td>
   <td>Compatibilidad</td>
  </tr>
  <tr>
   <td>Correo electrónico del recordatorio</td>
   <td>No compatible</td>
   <td>Compatibilidad</td>
  </tr>
  <tr>
   <td>Cambiar título en tiempo de espera de tarea</td>
   <td>No compatible</td>
   <td>Compatibilidad</td>
  </tr>
  <tr>
   <td>Correo electrónico en la delegación de tareas y la solicitud de tarea</td>
   <td>No compatible</td>
   <td>Compatibilidad</td>
  </tr>
  <tr>
   <td>Delegar entre grupos separados</td>
   <td>No compatible</td>
   <td>Compatibilidad</td>
  </tr>
  <tr>
   <td>Transformación XSLT</td>
   <td>No compatible</td>
   <td>Compatibilidad</td>
  </tr>
  <tr>
   <td>Prioridad de tareas dinámicas</td>
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

1. Puede utilizar Flujos de trabajo de AEM centrados en formularios en OSGi para firmar un formulario adaptable rellenado. Los flujos de trabajo de AEM centrados en formularios en OSGi son compatibles con la firma fuera del formulario. La variable [firma en formulario](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) experiencia no es compatible.

1. Es necesario acceder a AEM Bandeja de entrada para ejecutar y supervisar los flujos de trabajo centrados en formularios en AEM Forms OSGi y el espacio de trabajo de HTML para ejecutar y supervisar los flujos de trabajo de AEM Forms JEE.
1. Los servicios de documentos nativos de AEM Forms están disponibles para los flujos de trabajo AEM centrados en formularios en OSGi y AEM Forms en los flujos de trabajo JEE. AEM flujo de trabajo utiliza servicios de documentos nativos para flujos de trabajo AEM centrados en formularios en los flujos de trabajo OSGi y AEM Forms JEE (Process Management).
1. Los flujos de trabajo de AEM Forms JEE solo pueden procesar un formulario adaptable. No admite la representación de un formulario adaptable como documento PDF.
1. AEM formularios JEE Los flujos de trabajo no tienen un paso independiente para Adobe Sign. Se necesita un formulario adaptable habilitado para Adobe Sign para AEM formularios JEE Workflows. Para obtener más información, consulte [Documentación de Adobe Sign](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. Puede usar la variable [Invocar el servicio del modelo de datos del formulario](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) paso para invocar un servicio Web y publicar o recuperar datos de una aplicación de terceros.
1. Puede usar la variable [Enviar correo electrónico](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) paso para enviar correos electrónicos.

## Diferencias entre AEM bandeja de entrada y las funciones de la aplicación de AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Dos de las principales formas de iniciar un flujo de trabajo centrado en Forms son [Bandeja de entrada AEM](../../forms/using/manage-applications-inbox.md) y la aplicación AEM Forms. Sin embargo, las capacidades de AEM aplicación Inbox y AEM Forms difieren. AEM bandeja de entrada solo funciona con [Flujos de trabajo centrados en Forms](../../forms/using/aem-forms-workflow.md) mientras que la aplicación de AEM Forms funciona tanto con flujos de trabajo centrados en Forms como con la administración de procesos.

La tabla siguiente muestra las capacidades de AEM aplicación Bandeja de entrada y AEM Forms:

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
   <td><p>Compatibilidad</p> </td>
   <td><p>No compatible</p> </td>
  </tr>
  <tr>
   <td><p>Historial de tareas de seguimiento y resumen de tareas</p> </td>
   <td><p>Compatibilidad</p> </td>
   <td><p>No compatible</p> </td>
  </tr>
  <tr>
   <td><p>Adición de archivos adjuntos de nivel de tarea</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
  <tr>
   <td><p>Visualización de archivos adjuntos en el nivel de tarea</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
  <tr>
   <td><p>Adición de archivos adjuntos de nivel de campo</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
  <tr>
   <td><p>Visualización de la vista de calendario</p> </td>
   <td><p>Compatibilidad</p> </td>
   <td><p>No compatible</p> </td>
  </tr>
  <tr>
   <td><p>Adición de comentarios</p> </td>
   <td><p>Compatible</p> </td>
   <td><p>Compatible</p> </td>
  </tr>
 </tbody>
</table>
