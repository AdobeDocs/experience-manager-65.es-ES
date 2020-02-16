---
title: Acciones y capacidades de flujos de trabajo de AEM centrados en formularios en los flujos de trabajo de OSGi y AEM Forms JEE
seo-title: Acciones y capacidades de flujos de trabajo de AEM centrados en formularios en los flujos de trabajo de OSGi y AEM Forms JEE
description: nulo
seo-description: nulo
uuid: 8af9527d-fa5e-4fcb-88e1-49571528fca6
contentOwner: khsingh
topic-tags: publish
discoiquuid: 89bcc76d-122f-4a3f-b857-16e5376e1624
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe

---


# Acciones y capacidades de flujos de trabajo de AEM centrados en formularios en los flujos de trabajo de OSGi y AEM Forms JEE {#actions-and-capabilities-of-form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

## Bandeja de entrada de AEM y espacio de trabajo HTML {#aem-inbox-and-html-workspace}

La Bandeja de entrada de AEM se utiliza para ejecutar y supervisar flujos de trabajo de AEM centrados en formularios en OSGi. HTML Workspace le permite ejecutar y supervisar flujos de trabajo JEE de AEM Forms. En la tabla siguiente se enumeran las acciones importantes disponibles en la Bandeja de entrada de AEM para flujos de trabajo de AEM centrados en formularios en OSGi y en el espacio de trabajo HTML para flujos de trabajo JEE de AEM Forms.

<table>
 <tbody>
  <tr>
   <td>Acciones</td>
   <td>Bandeja de entrada AEM</td>
   <td>Espacio de trabajo HTML</td>
  </tr>
  <tr>
   <td>Inicio de un proceso, tarea o aplicación de formulario<br /> </td>
   <td>Admitido<br /> </td>
   <td>Admitido<br /> </td>
  </tr>
  <tr>
   <td>Envío de tareas</td>
   <td>Admitido<br /> </td>
   <td>Admitido<br /> </td>
  </tr>
  <tr>
   <td>Asignación de una tarea a un grupo</td>
   <td>Admitido<br /> </td>
   <td>Admitido<br /> </td>
  </tr>
  <tr>
   <td>Envío a varias rutas</td>
   <td>Admitido<br /> </td>
   <td>Admitido<br /> </td>
  </tr>
  <tr>
   <td>Historial de tareas de seguimiento y resumen de tareas</td>
   <td>Admitido<br /> </td>
   <td>Admitido<br /> </td>
  </tr>
  <tr>
   <td>Notificaciones por correo electrónico</td>
   <td>Admitido<br /> </td>
   <td>Admitido<br /> </td>
  </tr>
  <tr>
   <td>Reasignación de tareas</td>
   <td>Admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Datos adjuntos a nivel de campo para formularios adaptables</td>
   <td>Admitido</td>
   <td>No admitido</td>
  </tr>
  <tr>
   <td>Vista de calendario</td>
   <td>Admitido</td>
   <td>No admitido</td>
  </tr>
  <tr>
   <td>Comentarios de nivel de tarea</td>
   <td>Admitido</td>
   <td>No admitido</td>
  </tr>
  <tr>
   <td>Colas (cola personal compartida, reclamar tareas de la cola)</td>
   <td>No admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Notificación fuera de la oficina</td>
   <td>No admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Asignación de una tarea a varios usuarios</td>
   <td>No admitido</td>
   <td>Admitido</td>
  </tr>
 </tbody>
</table>

## Flujos de trabajo de AEM centrados en formularios en flujos de trabajo de OSGi y AEM Forms JEE {#form-centric-aem-workflows-on-osgi-and-aem-forms-jee-workflows}

Los flujos de trabajo de AEM centrados en formularios en OSGi y AEM Forms JEE (AEM Forms en administración de procesos JEE) tienen un conjunto diferente de funciones. En la tabla siguiente se enumeran las funciones y la compatibilidad importantes disponibles para las funciones de los flujos de trabajo de AEM centrados en formularios en OSGi y AEM Forms en los flujos de trabajo JEE:

<table>
 <tbody>
  <tr>
   <td>Funciones</td>
   <td>Flujos de trabajo de AEM centrados en formularios en OSGi<br /> </td>
   <td>Flujos de trabajo JEE de AEM Forms</td>
  </tr>
  <tr>
   <td>Formularios adaptables</td>
   <td>Admitido</td>
   <td>Admitido<br /> </td>
  </tr>
  <tr>
   <td>Integración con otras soluciones de AEM</td>
   <td>Admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Firma de garabatos (obsoleta)</td>
   <td>Admitido</td>
   <td>Admitido<br /> </td>
  </tr>
  <tr>
   <td>Plantillas de correo electrónico personalizadas</td>
   <td>Admitido</td>
   <td>Admitido<br /> </td>
  </tr>
  <tr>
   <td>Definición de la prioridad de tarea</td>
   <td>Admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Tiempo de espera de una tarea después de la fecha de vencimiento</td>
   <td>Admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Bucles dentro del flujo de trabajo</td>
   <td>Admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Selección dinámica de un usuario asignado </td>
   <td>Admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Uso de metadatos personalizados</td>
   <td>Admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Firma electrónica (Adobe Sign)</td>
   <td>Admitido <sup>[1]</sup></td>
   <td>Admitido <sup>[5]</sup></td>
  </tr>
  <tr>
   <td>Administración de tareas y aplicaciones de formularios</td>
   <td>Admitido <sup>[2]</sup><br /> </td>
   <td>Admitido <sup>[2]</sup></td>
  </tr>
  <tr>
   <td>Servicios de documentos</td>
   <td>Admitido <sup>[3]</sup></td>
   <td>Admitido <sup>[3]</sup></td>
  </tr>
  <tr>
   <td>Representar la tarea completada como formulario adaptable o documento PDF</td>
   <td>Admitido</td>
   <td>Admitido [4]</td>
  </tr>
  <tr>
   <td>Integración con la administración de correspondencia</td>
   <td>Admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Botón Restablecer</td>
   <td>Admitido</td>
   <td>No admitido</td>
  </tr>
  <tr>
   <td>Fases de flujo de trabajo</td>
   <td>Admitido</td>
   <td>No admitido</td>
  </tr>
  <tr>
   <td>Formularios adaptables de solo lectura</td>
   <td>Admitido</td>
   <td>No admitido</td>
  </tr>
  <tr>
   <td>Ocultar el botón de guardado predeterminado</td>
   <td>Admitido</td>
   <td>No admitido</td>
  </tr>
  <tr>
   <td>Control granular sobre la sección de detalles del flujo de trabajo</td>
   <td>Admitido</td>
   <td>No admitido</td>
  </tr>
  <tr>
   <td>Formularios HTML5, formularios PDF interactivos, conjunto de formularios<br /> </td>
   <td>Not Supported<br /> </td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Informes de procesos</td>
   <td>Not Supported<br /> </td>
   <td>Admitido<br /> </td>
  </tr>
  <tr>
   <td>Firma digital</td>
   <td>Admitido<br /> </td>
   <td>Admitido<br /> </td>
  </tr>
  <tr>
   <td>Categorías de puntos de partida</td>
   <td>No admitido </td>
   <td>Admitido </td>
  </tr>
  <tr>
   <td>Aprobación de tareas masivas </td>
   <td>No admitido </td>
   <td>Admitido </td>
  </tr>
  <tr>
   <td>Guardar borrador con un nombre personalizado</td>
   <td>No admitido </td>
   <td>Admitido </td>
  </tr>
  <tr>
   <td>Iniciar un proceso con los datos de proceso existentes<br /> </td>
   <td>No admitido</td>
   <td>Admitido </td>
  </tr>
  <tr>
   <td>Guardar un punto de partida como borrador</td>
   <td>No admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>avatar de usuario</td>
   <td>Admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Vista del administrador</td>
   <td>No admitido</td>
   <td>Admitido<br /> </td>
  </tr>
  <tr>
   <td>Plantillas de búsqueda</td>
   <td>No admitido</td>
   <td>Admitido<br /> </td>
  </tr>
  <tr>
   <td>Integración con aplicaciones de terceros</td>
   <td>Not Supported <sup>[6]</sup></td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Datos adjuntos de nivel de tarea para la aplicación de flujo de trabajo o el punto de inicio</td>
   <td>No admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Correo electrónico del recordatorio</td>
   <td>No admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Cambiar título en tiempo de espera de tarea</td>
   <td>No admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Correo electrónico en la delegación de tareas y notificación de tareas</td>
   <td>No admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Enviar un correo electrónico al final del flujo de trabajo</td>
   <td>Admitido <sup>[7]</sup></td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Delegar entre grupos desunidos</td>
   <td>No admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Llamar a un servicio Web desde un flujo de trabajo</td>
   <td>No admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Transformación XSLT</td>
   <td>No admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Gateways, SIN ESPERANZA </td>
   <td>Admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>O, Y Dividir</td>
   <td>No admitido</td>
   <td>Admitido</td>
  </tr>
  <tr>
   <td>Prioridad de tareas dinámicas</td>
   <td>No admitido</td>
   <td>No admitido</td>
  </tr>
 </tbody>
</table>

1. Puede utilizar Flujos de trabajo de AEM centrados en formularios en OSGi para firmar un formulario adaptable ya rellenado. Los flujos de trabajo de AEM centrados en el formulario en OSGi son compatibles con la firma fuera del formulario. No se admite la experiencia [de firma](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience) en el formulario.

1. Es necesario acceder a la Bandeja de entrada de AEM para ejecutar y controlar los flujos de trabajo de AEM Forms OSGi AEM y el espacio de trabajo HTML para ejecutar y supervisar los flujos de trabajo de JEE de AEM Forms.
1. AEM Forms Document Services nativo está disponible para flujos de trabajo de AEM centrados en el formulario en OSGi y AEM Forms en flujos de trabajo JEE. AEM Workflow utiliza servicios de documentos nativos para flujos de trabajo de AEM centrados en formularios en flujos de trabajo OSGi y AEM Forms JEE (Process Management).
1. Los flujos de trabajo JEE de AEM Forms solo pueden procesar un formulario adaptable. No admite el procesamiento de un formulario adaptable como documento PDF.
1. Los flujos de trabajo JEE de formularios AEM no tienen un paso independiente para Adobe Sign. Se requiere un formulario adaptable habilitado para Adobe Sign para los flujos de trabajo JEE de formularios AEM. Para obtener más información, consulte la documentación [de](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component)Adobe Sign.
1. Puede utilizar el paso [Invocar el servicio](../../forms/using/aem-forms-workflow-step-reference.md#p-invoke-form-data-model-service-step-p) del modelo de datos de formulario para invocar un servicio Web y publicar o recuperar datos de una aplicación de terceros.
1. Puede utilizar el paso [Enviar correo electrónico](../../forms/using/aem-forms-workflow-step-reference.md#send-email-step) para enviar correos electrónicos.

## Diferencias entre las funciones de la bandeja de entrada de AEM y de la aplicación de AEM Forms {#differences-between-aem-inbox-and-aem-forms-app-features}

Dos de las formas más importantes de iniciar un flujo de trabajo centrado en formularios son utilizar la bandeja de entrada [de](../../forms/using/manage-applications-inbox.md) AEM y la aplicación de AEM Forms. Sin embargo, las funciones de la bandeja de entrada de AEM y de la aplicación de AEM Forms difieren. La bandeja de entrada de AEM solo funciona con flujos de trabajo [centrados en](../../forms/using/aem-forms-workflow.md) Forms, mientras que la aplicación de AEM Forms funciona tanto con flujos de trabajo centrados en Forms como con la gestión de procesos.

En la tabla siguiente se muestran las funciones de la bandeja de entrada de AEM y de la aplicación de AEM Forms:

<table>
 <tbody>
  <tr>
   <td><p><strong>Acciones</strong></p> </td>
   <td><p><strong>Bandeja de entrada AEM</strong></p> </td>
   <td><p><strong>Aplicación de AEM Forms</strong></p> </td>
  </tr>
  <tr>
   <td><p>Inicio de una aplicación de formulario</p> </td>
   <td><p>Admitido</p> </td>
   <td><p>Admitido</p> </td>
  </tr>
  <tr>
   <td><p>Envío de tareas</p> </td>
   <td><p>Admitido</p> </td>
   <td><p>Admitido</p> </td>
  </tr>
  <tr>
   <td><p>Delegación de tareas</p> </td>
   <td><p>Admitido</p> </td>
   <td><p>No admitido</p> </td>
  </tr>
  <tr>
   <td><p>Historial de tareas de seguimiento y resumen de tareas</p> </td>
   <td><p>Admitido</p> </td>
   <td><p>No admitido</p> </td>
  </tr>
  <tr>
   <td><p>Adición de datos adjuntos de nivel de tarea</p> </td>
   <td><p>Admitido</p> </td>
   <td><p>Admitido</p> </td>
  </tr>
  <tr>
   <td><p>Visualización de datos adjuntos de nivel de tarea</p> </td>
   <td><p>Admitido</p> </td>
   <td><p>Admitido</p> </td>
  </tr>
  <tr>
   <td><p>Adición de datos adjuntos de nivel de campo</p> </td>
   <td><p>Admitido</p> </td>
   <td><p>Admitido</p> </td>
  </tr>
  <tr>
   <td><p>Visualización de la vista de calendario</p> </td>
   <td><p>Admitido</p> </td>
   <td><p>No admitido</p> </td>
  </tr>
  <tr>
   <td><p>Adición de comentarios</p> </td>
   <td><p>Admitido</p> </td>
   <td><p>Admitido</p> </td>
  </tr>
 </tbody>
</table>

