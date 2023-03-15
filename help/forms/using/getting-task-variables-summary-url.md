---
title: Obtener variables de tarea en la URL de resumen
seo-title: Getting Task Variables in Summary URL
description: Aprenda a reutilizar la información sobre una tarea y a generar una URL de resumen para resumir o describir una tarea.
seo-description: How-to reuse the information about a task and generate a Summary URL to summarize or describe a task.
uuid: 9eab3a6a-a99a-40ae-b483-33ec7d21c5b6
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 6dc31bec-b02d-47db-a4f4-be8c14c5619e
exl-id: b5e27b54-d141-48dd-a4ed-dd0a691319a5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 100%

---

# Obtener variables de tarea en la URL de resumen {#getting-task-variables-in-summary-url}

La página Resumen muestra información relacionada con las tareas. Este artículo describe cómo reutilizar la información relacionada con las tareas en la página Resumen.

En esta orquestación de ejemplo, un empleado envía un formulario de solicitud de baja. A continuación, el formulario de solicitud se envía al administrador del empleado para que lo apruebe.

1. Crear un procesador de HTML de ejemplo (html.esp) para resourseType **Empleados/PtoApplication**.

   El procesador asume las siguientes propiedades, que se deben establecer en el nodo:

   * ename
   * empid
   * reason
   * duration

   >[!NOTE]
   >
   >Este procesador es la plantilla de página Resumen.

   El siguiente código de ejemplo para este procesador está contenido en la siguiente ubicación:

   `apps/Employees/PtoApplication/html.esp`

   ```html
   <html>
     <body>
       <table>
       <tbody>
       <tr>
           <td>
               <h3>Employee Name: <%= currentNode.ename %></h3>
               <h3>Employee ID: <%= currentNode.eid %></h3>
               <h3>Leave duration: <%= currentNode.duration %> days</h3>
               <h3>Reason: <%= currentNode.reason %></h3>
           </td>
       </tr>
       </tbody>
       </table>
     </body>
   </html>
   ```

1. Modifique la orquestación para extraer las cuatro propiedades de los datos del formulario enviado. A continuación, cree un nodo en CRX de tipo **Employees/PtoApplication** con las propiedades rellenadas.

   1. Cree el proceso **Crear resumen de PTO** y utilícelo como subproceso antes de la operación **Asignar tarea** en su orquestación.
   1. Establezca **employeeName**, **employeeID**, **ptoReason**, **totalDays** y **nodeName** como las variables de entrada del nuevo proceso. Estas variables se pasarán como los datos de formulario enviados.

      Establezca también una variable de salida **ptoNodePath**, que se utilizará al configurar la URL de resumen.

   1. En el proceso **Crear resumen de PTO** proceso, utilice el componente **Establecer valor** para establecer los detalles de entrada en una asignación **nodeProperty**(**nodeProps**).

      Las claves de esta asignación deben ser las mismas que las establecidas en el procesador de HTML del paso anterior.

      Asimismo, agregue una clave **sling:resourceType** con el valor **Employees/PtoApplication** a la asignación.

   1. Utilice el subproceso **storeContent** del servicio **ContentRepositoryConnector** en el proceso **Crear resumen de PTO**. Este subproceso crea un nodo CRX.

      Toma tres variables de entrada:

      * **Ruta de carpeta**: la ruta en la que se crea el nuevo nodo CRX. Establezca la ruta como **/content**.
      * **Nombre del nodo**: asigne la variable de entrada nodeName a este campo. Es una cadena de nombre de nodo única.
      * **Tipo de nodo**: establezca el tipo como **nt:unstructured**. La salida de este proceso es nodePath. nodePath es la ruta CRX del nodo recién creado. ndoePath es la salida final del proceso **Crear resumen de PTO**.
   1. Pase los datos de formulario enviados (**employeeName**, **employeeID**, **ptoReason** y **totalDays**) como entrada al nuevo proceso **Crear resumen de PTO**. Tome la salida como **ptoSummaryNodePath**.


1. Defina la URL de resumen como una expresión XPath que contiene los detalles del servidor junto con **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

En AEM Forms Workspace, cuando se abre una tarea, la URL de resumen accede al nodo CRX, y el procesador de HTML muestra el resumen.

El diseño del resumen se puede cambiar sin modificar el proceso. El procesador de HTML muestra correctamente el resumen.
