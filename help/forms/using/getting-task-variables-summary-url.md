---
title: Obtención de variables de tarea en la URL de resumen
seo-title: Getting Task Variables in Summary URL
description: Cómo reutilizar la información sobre una tarea y generar una URL de resumen para resumir o describir una tarea.
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
ht-degree: 0%

---

# Obtención de variables de tarea en la URL de resumen {#getting-task-variables-in-summary-url}

La página de resumen muestra información relacionada con las tareas. En este artículo se describe cómo reutilizar la información relacionada con las tareas en la página de resumen.

En esta orquestación de ejemplo, un empleado envía un formulario de solicitud de baja. A continuación, el formulario de solicitud se envía al administrador del empleado para su aprobación.

1. Creación de un procesador de HTML de ejemplo (html.esp) para resourcesType **Empleados/PtoApplication**.

   El renderizador asume las siguientes propiedades que se deben establecer en el nodo :

   * Nombre
   * empid
   * reason
   * duration

   >[!NOTE]
   >
   >Este procesador es la plantilla de página de resumen.

   El siguiente código de ejemplo para este renderizador está contenido en:

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

1. Modifique la organización para extraer las cuatro propiedades de los datos del formulario enviados. Después de esto, cree un nodo en CRX de tipo **Empleados/PtoApplication**, con las propiedades rellenadas.

   1. Crear un proceso **crear resumen de PTO** y utilice esto como un subproceso antes de que **Asignar tarea** en su orquestación.
   1. Definir **employeeName**, **employeeID**, **ptoReason**, **totalDays** y **nodeName** como variables de entrada en el nuevo proceso. Estas variables se pasarán como datos de formulario enviados.

      Defina también una variable de salida **ptoNodePath** que se utilizará al configurar la URL de resumen.

   1. En el **crear resumen de PTO** proceso, utilice el **establecer valor** para definir los detalles de entrada en un **nodeProperty**(**nodeProps**).

      Las claves de este mapa deben ser las mismas que las definidas en el procesador del HTML en el paso anterior.

      Además, agregue un **sling:resourceType** clave con valor **Empleados/PtoApplication** en el mapa.

   1. Uso del subproceso **storeContent** de la variable **ContentRepositoryConnector** en el **crear resumen de PTO** proceso. Este subproceso crea un nodo CRX.

      Toma tres variables de entrada:

      * **Ruta de carpeta**: Ruta donde se crea el nuevo nodo CRX. Establezca la ruta como **/content**.
      * **Nombre del nodo**: Asigne la variable de entrada nodeName a este campo. Es una cadena de nombre de nodo única.
      * **Tipo de nodo**: Defina el tipo como **nt:unstructured**. El resultado de este proceso es nodePath. nodePath es la ruta CRX del nodo recién creado. La ruta de acceso del nodo sería el resultado final del **crear PTO** proceso de resumen.
   1. Transmita los datos del formulario enviado (**employeeName**, **employeeID**, **ptoReason** y **totalDays**) como entrada al nuevo proceso **crear resumen de PTO**. Tome la salida como **ptoSummaryNodePath**.


1. Defina la URL de resumen como una expresión XPath que contenga los detalles del servidor junto con **ptoSummaryNodePath**.

   XPath: `concat('https://[*server*]:[*port*]/lc',/process_data/@ptoSummaryNodePath,'.html')`.

En el espacio de trabajo de AEM Forms, cuando se abre una tarea, la dirección URL de resumen accede al nodo CRX y el procesador del HTML muestra el resumen.

El diseño del resumen se puede cambiar sin modificar el proceso. El procesador del HTML muestra el resumen correctamente.
